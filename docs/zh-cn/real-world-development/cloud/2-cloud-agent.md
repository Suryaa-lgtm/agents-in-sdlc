---
title: "练习 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义指令][previous-lesson] |
|:--|

几乎没有组织完全不存在技术债务。这可能包括未解决的安全问题、需要更新的遗留代码，或因没有时间实施而长期滞留在待办事项中的功能请求。GitHub Copilot cloud agent 可执行更新代码、添加功能等任务，并以自主方式工作。智能体完成工作后，会生成供人类开发人员审查的草稿 PR，从而分担重复性任务，加速开发，并让开发人员专注于更宏观的工作。

你将通过 Copilot cloud agent 探索：

- 自定义代码生成环境。
- 确保操作安全执行。
- 明确界定议题范围的重要性。
- 将议题分配给 Copilot。

## 场景

Tailspin Toys 希望解决一些技术债务。最初由承包商创建的首版网站文档状态不理想，甚至几乎完全缺失。第一步，团队希望为应用中所有导出的函数添加 TSDoc 文档注释。

此外，设计团队希望改善游戏发现体验。他们希望每个游戏详情页显示相关游戏，即同类别的其他游戏标题，方便用户继续浏览。当前不需要完善的实现，只需一个可用于用户体验验收测试的版本。这是当前阻塞之一，但还有一些优先级更高的议题。

这些任务都很适合交给 Copilot cloud agent。它可异步完成工作，让开发人员专注于其他任务；工作完成后再由开发人员审查，确认结果符合预期。

## 介绍 GitHub Copilot cloud agent

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) 可以像人类开发人员一样在后台执行任务，也可以通过[将 GitHub issue 分配给 Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions) 来启动工作。分配后，Copilot 会创建草稿拉取请求跟踪进度、建立环境并开始工作。你可以在会话进行中或完成后查看详情。当结果可供审查时，Copilot 会在拉取请求中通知你。

## 明确界定指令范围的重要性

GitHub Copilot 不会替你跳过思考。即使看似简单的操作，在深入后也可能包含复杂性，因此[为 Copilot cloud agent 明确界定任务范围][cloud-agent-best-practices]非常重要。可将它视为 AI 结对编程伙伴：分阶段工作、学习、试验并随时调整。增加生成式 AI 不会改变软件开发的基本原则。

## 本存储库中的自定义指令

前面的练习已介绍自定义指令及其引导 Copilot 的方式。如果已完成自定义指令实践，应该已经看到 `.github/copilot-instructions.md` 的效果；如果尚未完成，现在可以快速查看。在分配工作前，先只读查看存储库中的指令文件，以便稍后观察其影响。

在存储库的 GitHub Web UI 或正在运行的 Codespace 中打开：

- `.github/copilot-instructions.md`：审查 **Code standards** 部分，特别是 TypeScript 和 TSDoc 文档注释要求。
- `.github/instructions/unit-tests.instructions.md`：注意其 `applyTo` frontmatter，它将指令限定到 `**/*.test.ts` 文件。

下一节将 `Code lacks documentation` 议题分配给 cloud agent 后，请关注生成的拉取请求中的 TSDoc 注释、TypeScript 风格和注释头。

## 为 Copilot cloud agent 设置开发环境

无论由谁编写代码，通常都需要特定环境并运行设置脚本，以确保环境处于良好状态。向 Copilot 分配任务时同样如此。Cloud agent 使用 [GitHub Actions][github-actions] 作为工作环境。可通过 `.github/workflows/copilot-setup-steps.yml` 创建[专用设置工作流][setup-workflow]，在它开始工作前运行，以便访问所需开发工具和依赖项。实验已预先配置此流程，以确保 Copilot 能使用 Node.js、项目依赖项、端到端测试所需浏览器，以及这个单一 Astro 应用所需的迁移和种子 SQLite 数据库：

```yaml
name: "Copilot Setup Steps"

# 允许你从存储库的“Actions”选项卡测试设置步骤
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 将权限设为这些步骤所需的最低权限。Copilot 会获得自己的令牌来执行操作。
    permissions:
      # 如果设置步骤需要克隆存储库（例如安装依赖项），则需要 `contents: read` 权限。如果未在设置步骤中克隆存储库，Copilot 会在步骤完成后自动克隆。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # 前端/应用设置 - Node.js（整个应用现在是 Astro + Drizzle/libSQL）
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # 迁移并填充本地 SQLite 数据库，以便构建和测试有可用数据。
      - name: Set up the database
        run: npm run db:setup
```

该文件看起来与其他 GitHub 工作流文件相似，但有几个关键点：

- 包含名为 `copilot-setup-steps` 的单个作业。
- 作业在 Copilot 开始处理拉取请求前由 GitHub Actions 执行。
- `workflow_dispatch` 触发器允许从存储库的 **Actions** 选项卡手动运行工作流，便于测试环境而无需等待 Copilot。

## 添加文档

所有人都知道文档的重要性，但多数项目的文档要么过时，要么完全缺失。这类技术债务经常得不到处理，会降低生产力，使代码库更难维护，并增加新开发人员的接手成本。Copilot 擅长创建文档，因此这是交给 Copilot cloud agent 的理想议题。它会在后台生成所需文档，稍后由你审查。

1. 在新的浏览器标签页中打开 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 创建议题。
5. 将 **Title** 设置为 `Code lacks documentation`。
6. 将 **Description** 设置为：

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot** 打开分配对话框。

   ![将 Copilot 分配给议题](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

   ![Copilot 议题分配详情](../../../_images/ex4-assign-copilot-details.png)

10. 打开 **Pull Requests** 选项卡。
11. 打开新生成的拉取请求，标题可能类似 `[WIP]: Code lacks documentation`。如果列表中尚未出现，请稍候并刷新。
12. 几分钟后，应能看到 Copilot 创建了待办事项列表。

> [!NOTE]
> Copilot 在 PR 中显示待办事项可能需要几分钟。它会创建环境、分析项目并确定解决问题的最佳方案。

13. 审查列表及计划执行的任务。
14. 在拉取请求时间线中向下滚动，应能看到 Copilot 已开始处理议题。
15. 选择 **View session**。

   ![Copilot 会话视图](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 如看不到更新后的状态，请刷新窗口。

16. 查看实时会话：包括探索代码、理解状态、暂停思考并决定方案，以及创建代码。

这个过程可能需要几分钟。Copilot cloud agent 的主要目标之一是异步执行任务，让你专注于其他工作。现在可利用这一优势：将另一项任务分配给 cloud agent，同时转而编写代码并为应用添加功能。

## 在游戏详情页添加相关游戏部分

为设计团队添加相关游戏部分可能不会耗时太久，但这段时间可用于其他任务。让 Copilot cloud agent 来完成！

1. 返回 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue**。
5. 将 **Title** 设置为 `Show related games on the game details page`。
6. 将 **Description** 设置为：

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot** 打开分配对话框。

   ![将 Copilot 分配给议题](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

不久后，议题第一条评论应出现一组 👀，表示 Copilot 正在处理！

![Copilot 使用眼睛表情符号表示正在处理议题](../../../_images/ex4-issue-eyes-emoji.png)

Copilot 正在认真处理第二项请求！Copilot cloud agent 的工作方式与软件工程师相似，因此无需持续监控；等它完成后再审查即可。现在可以转而创建和使用自定义智能体。

## 总结与后续步骤

本课探索了 [GitHub Copilot cloud agent][copilot-agents]。通过 cloud agent，可异步分配议题给 Copilot，以处理技术债务、创建新功能或迁移框架。

你探索了以下概念：

- 自定义代码生成环境。
- 确保操作安全执行。
- 明确界定议题范围的重要性。
- 将议题分配给 Copilot。

cloud agent 在后台工作时，我们可以转而创建并使用自定义智能体。[Copilot cloud agent 也可使用 MCP 服务器][cloud-agent-mcp]，并可读取此前已探索的自定义指令。

## 资源

- [关于 Copilot cloud agent][copilot-agents]
- [将 GitHub issues 分配给 Copilot][assign-issue]
- [Copilot cloud agent 设置工作流最佳实践][cloud-agent-best-practices]

| [下一课：自定义智能体 →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
