---
title: "练习 5：迭代 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

## 审查工作

在本实验中，你使用 GitHub Copilot 完成了多项改善用户体验和新增功能的任务：要求它为代码添加文档、构建供设计团队迭代的相关游戏功能，以及实现高对比度和浅色模式切换等无障碍功能。下面审查代码更改，并在必要时向 Copilot 提供反馈。

### 场景

软件设计和 DevOps 的基本原则不会因生成式 AI 的加入而改变。始终应审查生成的代码并遵循正常的 DevOps 流程。接下来，在向其余团队成员开启审查前，审查 Copilot 为文档、相关游戏功能和无障碍功能提出的建议。

## 安全与 GitHub Copilot cloud agent

由于 Copilot cloud agent 异步且无人监督地执行任务，系统设置了若干安全限制：

- Copilot 对存储库只有读取权限，对代码分支只有写入权限。
- Cloud agent 在 GitHub Actions 内运行，并创建独立、临时的工作环境。
- 任何 GitHub Actions 工作流运行前都需要人工批准。
- [默认限制对外部资源的访问][agent-firewall]，包括 MCP 服务器。

## 审查生成的文档

先审查 GitHub Copilot cloud agent 生成的第一个拉取请求，即为代码添加文档。

> [!NOTE]
> 查看 PR 时可能看到防火墙阻止 Copilot 的警告。这是预期行为，因为 cloud agent 默认限制外部资源访问，包括外部 MCP 服务器。若需要，可[自定义或关闭防火墙][agent-firewall]。

1. 返回 github.com 上的存储库。
2. 选择 **Pull Requests** 打开 PR 列表。
3. 打开标题类似 **Add missing documentation** 或更具体的拉取请求。

> [!NOTE]
> 如果 Copilot 仍在处理任务，PR 会带有 **[WIP]** 标记。此时等待 Copilot 完成，可能需要几分钟。

4. 准备就绪后，选择 **Files changed** 选项卡审查更改。

   ![Files changed 选项卡](../../../_images/shared-pr-files-changed.png)

5. 检查新更新的代码，其中应包含 TSDoc 文档注释和其他文档。实际更改可能有所不同。

   审查时关注 TSDoc 文档注释、TypeScript 风格和注释头。它们来自练习 2 开始时审查的自定义指令文件。

6. 确信更新无误后返回 **Conversation** 选项卡并向下滚动。
7. 应能看到某些工作流正在等待批准。
8. 如果工作流正在等待批准，选择 **Approve and run workflows**。

   ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

9. 工作流应进入 PR 检查队列。正常情况下，该单一 Astro 应用的项目检查会通过。完成可能需要几分钟。

## 请 GitHub Copilot 请求更改

与 Copilot 协作处理拉取请求并非单向过程。你可以像标记其他团队成员一样，在 PR 评论或代码行内评论中标记 Copilot。Copilot 会读取这些评论，并启动新会话来处理请求。由于生成结果具有不确定性，无法提供适用于所有情况的固定提示文本。可以请 Copilot：

- 为每个代码文件顶部添加简短说明用途的注释头。
- 为 TypeScript 和 Astro 文件添加 TSDoc 文档注释。
- 创建说明 Astro 应用结构的 README。

1. 在评论中请求修改生成的文档，并像标记其他用户一样标记 **@copilot**。可以采用上面列出的建议，也可以提出其他希望在代码库中看到的文档改进。
2. 选择 **View Session**，观察 Copilot 执行修改。注意 Copilot 会启动新会话来进行更新。

   ![返回拉取请求](../../../_images/ex7-back-to-pr.png)

3. 你可以选择 **Back to pull request** 返回拉取请求。
4. Copilot 完成更改后，PR 中应出现新提交。
5. 选择 **Files changed** 选项卡审查更改。

可持续迭代直至满意。满意后将 PR 从草稿转换为待审查状态，并合并到主分支。

![将 PR 转换为待审查状态](../../../_images/ex7-ready-for-review.png)

## 审查相关游戏功能

下面审查 Copilot 为在游戏详情页显示相关游戏而生成的 PR。

1. 返回 github.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Show related games on the game details page** 或更具体的 PR。
4. 选择 **Files changed** 选项卡审查生成的代码。
5. 审查完毕且一切正常后，返回 **Conversation** 选项卡并向下滚动。
6. 查看是否有工作流等待批准。
7. 如果有工作流等待批准，选择 **Approve and run workflows**。

   ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

8. 工作流应在 PR 的检查部分排队运行。正常情况下，单个 Astro 应用的项目检查会通过。完成可能需要几分钟。
9. **可选：**也可以在 Codespace 中切换到此分支，手动测试相关游戏功能。打开 Codespace 终端并运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名，例如 **copilot/fix-8**）：

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Copilot 已构建相关游戏功能！与之前一样，你可以继续迭代 cloud agent 的工作，例如请求调整显示的相关游戏数量，或要求补充注释头和 TSDoc 文档注释（请记住，分配这项任务时，你还没有更新自定义指令）。同样，可以在 **Conversation** 选项卡添加评论，Copilot 会读取评论并启动新会话。

## 审查无障碍功能

最后审查使用自定义无障碍智能体实现的功能。该 PR 应包含练习 3 中分配的高对比度模式，以及练习 4 中在 Mission Control 请求的浅色模式。

1. 返回 github.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Add high contrast mode to website** 或更具体的 PR。

> [!NOTE]
> 如果 Copilot 仍在处理任务，PR 会带有 **[WIP]** 标记，请等待几分钟完成。

4. 选择 **Files changed** 审查生成的代码。
5. 审查实现，重点关注：
   - 用于切换模式的 UI 组件。
   - 使用本地存储保存用户偏好。
   - 高对比度和浅色模式的 CSS 或样式更改。
   - 无障碍属性（ARIA 标签、键盘导航等）。
   - 管理模式切换的 JavaScript/TypeScript 代码。

6. 审查完毕且一切正常后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有工作流等待批准。
8. 如果有工作流等待批准，选择 **Approve and run workflows**。

   ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

9. 工作流应在 PR 的检查部分排队运行。正常情况下，单个 Astro 应用的项目检查会通过。完成可能需要几分钟。
10. **可选：**可以在 Codespace 中切换到该分支，手动测试无障碍功能。打开 Codespace 终端并运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名）：

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

   启动应用，在浏览器中测试高对比度和浅色模式切换，确认模式在页面重新加载后仍然保留。

自定义无障碍智能体帮助 Copilot 按无障碍最佳实践实现这些功能。如发现无障碍问题或改进空间，可像此前一样在评论中标记 **@copilot** 请求更新。

## 可选练习：持续委托

Cloud agent 最适合处理真实待办事项。可在存储库中创建更多议题并分配给 Copilot，例如：

- 在游戏详情页创建支持者兴趣表单。
- 在游戏列表页实现分页。
- 为数据访问辅助函数添加输入验证和错误处理。

## 总结

你已完成 Cloud agent 学习路径。本系列中，你：

- 检查了存储库附带的自定义指令，并观察其在 cloud agent 输出中的效果。
- 将议题分配给 Copilot cloud agent，并观察其异步设置环境、规划和执行。
- 创建并使用了无障碍自定义智能体，添加高对比度和浅色模式切换。
- 使用 Copilot 智能体页面作为 Mission Control，监控并在会话进行中引导无障碍工作。
- 审查并迭代 cloud agent 的拉取请求，通过 `@copilot` 请求更改并批准工作流。

## 审查与后续步骤

Cloud agent 学习路径已经完成。其他学习路径可与此处实践互补：

- 🖥️ **[VS Code 学习路径](../../vscode/)** — 直接在 IDE 中探索 Copilot Chat 智能体模式和 MCP 集成。
- 💻 **[CLI 学习路径](../../cli/)** — 在终端中交付两项经过审查的更改，使用 Plan 和 Autopilot、智能体技能、自定义 QA 智能体、Playwright MCP、Agent Merge，以及可选的 `/delegate` cloud delegation。

在自己的存储库中可尝试：

- 将重构或测试覆盖率议题分配给 cloud agent。
- 为其他领域创建自定义智能体。
- 为不同技术栈设置 `copilot-setup-steps.yml`。

## 资源

- [GitHub Copilot][github-copilot]
- [关于 Copilot 智能体][copilot-agents]
- [将 GitHub issues 分配给 Copilot][assign-issue]
- [Copilot cloud agent 设置工作流最佳实践][cloud-agent-best-practices]
- [配置 Copilot cloud agent 防火墙][agent-firewall]

| [← 上一课：管理智能体][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
[previous-lesson]: ../4-managing-agents/
