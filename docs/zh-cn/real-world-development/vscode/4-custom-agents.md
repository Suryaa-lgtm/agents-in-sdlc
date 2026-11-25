---
title: "练习 4 - 自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

[GitHub Copilot 中的自定义智能体][custom-agents-concept]可根据开发工作流中的特定任务或领域，创建专门的 AI 助手。通过在存储库的 `.github/agents` 文件夹中使用 Markdown 文件定义智能体，可以为 Copilot 提供针对性的指令、最佳实践、编码模式和领域知识，从而引导它更有效地完成特定类型的工作。团队可以将专业知识编写成可复用的智能体，例如执行 [WCAG][wcag] 合规性要求的无障碍智能体、遵循安全编码实践的安全智能体，或维护一致测试模式的测试智能体。

自定义智能体由项目 `.github/agents` 文件夹中的 Markdown 文件定义，也可以全局定义在 `~/.copilot/agents` 中。每个文件都包含 YAML frontmatter，至少需要 `name` 和 `description` 字段；后面则是定义智能体行为、专业知识和指令的 Markdown 提示词。

### 自定义智能体与智能体技能

自定义智能体与[智能体技能][agent-skills-concept]在概念上有些重叠。两者主要都通过 Markdown 文件定义，并告诉 AI 如何执行操作。最简单的区分方式是：**自定义智能体是执行者，技能是工具**。

自定义智能体拥有自己的上下文窗口，并负责协调技能（甚至其他智能体）来完成工作。在本练习中，无障碍自定义智能体会根据无障碍指南审查和更新网站；在执行过程中，它可以调用拉取请求工作流技能，或运行和管理测试的技能。

> [!NOTE]
> 编写自定义智能体没有唯一正确的方式。与 AI 相关的其他工作一样，应通过测试和迭代，找到适合当前环境和场景的方法。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## 场景

Tailspin Toys 致力于确保所有用户都能访问其众筹平台，无论用户的视觉能力或偏好如何。近期用户反馈指出，当前深色主题中的文本与背景颜色对比度不足，导致部分用户难以阅读。为解决这个无障碍问题，设计团队要求实现可由用户开启或关闭的高对比度模式。

无障碍性至关重要，因此希望尽快实现此功能。你将使用自定义智能体生成实现。

本练习将介绍如何：

- 审查现有的无障碍自定义智能体。
- 在 Copilot Chat 中使用无障碍智能体实现高对比度模式。

## 审查无障碍自定义智能体

存储库已为无障碍工作预先创建了一个自定义智能体。先审查其内容，了解它将如何引导 Copilot。

返回 Codespace，打开终端，并从 `main` 创建专用于无障碍工作的分支（这样可以将筛选 PR 与本练习分开）：

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. 打开 `.github/agents/accessibility.md`。
2. 注意包含 `name` 和 `description` 字段的 YAML frontmatter。

> [!CAUTION]
> 自定义智能体必须包含 `name` 和 `description` frontmatter。

3. 浏览并查看后续部分，了解其中介绍的内容：
   - 为无障碍网站生成代码时的核心职责。
   - 无障碍最佳实践。
   - HTML、CSS 和 JavaScript 代码示例。
   - 常见陷阱和错误列表。

## 在 Copilot Chat 中使用自定义智能体

VS Code 会在 Copilot Chat 视图底部的智能体下拉列表中显示 `.github/agents` 中定义的每个自定义智能体。选择自定义智能体后，该聊天会话将使用此智能体的指令和工具。

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，以开始全新的对话。不同练习所需的模式和模型可能不同；每个步骤会在适用时说明。

1. 如果 Chat 视图的智能体下拉列表中尚未选择 **Agent**，请选择它。

   ![Chat 视图中智能体选择器的屏幕截图。](../../../_images/shared-chat-mode-selector.png)

2. 选择 Chat 视图底部的智能体下拉列表（其中会显示当前使用的智能体，默认是 **default**）。
3. 在可用智能体列表中选择 **Accessibility agent**。
4. 向无障碍智能体发送以下提示词：

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

5. Copilot Chat 会开始工作：探索代码库、提出更改并修改项目文件。每项编辑都会在聊天中内嵌显示文件路径和差异，供你审查。
6. 随着编辑逐步应用，**Files changed** 指示器会更新，显示智能体修改的工作集。

> [!NOTE]
> 此过程可能需要几分钟。Copilot 会实际修改存储库文件，例如 Astro 组件、CSS 和相关测试。

下一课将审查并引导这项正在进行的工作。

## 总结与后续步骤

本课介绍了 GitHub Copilot 中面向特定任务和领域的专业 AI 助手——[自定义智能体][custom-agents]。自定义智能体可将团队的专业知识和标准编写成可复用的智能体，引导 Copilot 更有效地完成特定类型的工作。

你探索了以下内容：

- 如何定义自定义智能体。
- 如何在 Copilot Chat 的智能体模式中使用自定义智能体。

接下来，你将[监控并引导智能体的工作][next-lesson]：审查实时更改，并在同一个会话中添加浅色模式切换。

## 资源

- [关于自定义智能体][custom-agents]
- [在 IDE 中创建自定义智能体][creating-custom-agents-ide]
- [VS Code 中的自定义智能体][custom-agents-vscode]
- [自定义智能体配置][custom-agents-config]
- [awesome-copilot 中的自定义智能体][awesome-copilot-agents]

---

| [← 上一课：使用 Playwright MCP 服务器测试功能][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
