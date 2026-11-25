---
title: "练习 5 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义智能体][previous-lesson] |
|:--|

将 GitHub Copilot 置于智能体模式后，它会自主探索代码库、提出更改、编辑文件并运行命令。由于工作实时发生在当前计算机上，VS Code 中的 Copilot Chat 会实时显示每一次工具调用和文件编辑。每次文件编辑都会在聊天中内嵌显示差异，并提供 **Keep** 和 **Undo** 控件。你可以审查每个差异、接受或拒绝单项更改，并通过后续提示在不离开编辑器的情况下调整或扩展工作。

本练习将：

- 实时监控无障碍智能体的工作。
- 审查并接受提议的文件编辑。
- 在会话进行中引导智能体添加浅色模式切换。

## 场景

[练习 4][previous-lesson]中的无障碍自定义智能体正在实现高对比度模式。工作进行期间，设计团队提出附加要求：为觉得默认主题过暗的用户添加浅色模式切换。无需重新开始对话，可直接引导现有会话扩展功能。

## 监控 Copilot 的进度

Copilot Chat 会显示智能体执行的每一步：探索的文件、运行的命令和提议的编辑。

1. 返回练习 4 使用的 Copilot Chat。
2. 智能体工作时，查看聊天中的每次工具调用，包括文件读取、文件编辑和终端命令。
3. 智能体提议文件编辑时，差异会内嵌显示：
   - 选择 **Keep**接受更改。
   - 选择 **Undo**撤销更改并让智能体重做。
4. 可打开聊天顶部的 **Files changed**查看本次会话中修改的全部文件。

> [!NOTE]
> 如果工具调用请求权限（例如运行终端命令），智能体会暂停并显示 **Allow** 提示。只批准你确认安全的命令。

5. 等待智能体完成高对比度模式实现，并查看总结其更改的最终消息。

## 引导智能体添加浅色模式

高对比度模式就位后，在同一对话中继续添加浅色模式切换。智能体会保留组件、样式和本地存储模式等之前的上下文。

1. 在 Copilot Chat 输入框发送：

   ```plaintext
   Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
   ```

2. 智能体会基于已有更改提出浅色模式改动。
3. 与审查高对比度更改一样逐项审查差异，并选择 **Keep**或 **Undo**。
4. 如智能体的方向不符合预期，可选择聊天输入框旁的 **Stop**停止，再发送澄清提示。

> [!TIP]
> 引导进行中的会话比重新开始更快。可使用后续提示进行调整（例如“简化 CSS，改用 CSS 变量，不要重复选择器”）、纠正方向（例如“不要添加第三个切换开关，把浅色模式集成到现有设置面板中”），或扩展范围（例如“同时为两个切换开关添加键盘快捷键”）。

## 审查工作集

提交前快速检查智能体修改的全部内容。

1. 在 VS Code 中打开 **Source Control**。
2. 审查已更改文件的完整列表，应包含 Astro 组件、样式及相关测试。
3. 打开部分文件并逐项检查差异，确认无障碍模式包括 ARIA 属性、键盘导航、语义化 HTML 和本地存储持久化。
4. 满意后，在 Source Control 中暂存并提交更改；下一课将发布更改。

## 总结与后续步骤

你使用 Copilot Chat 智能体模式实时监控并引导进行中的会话：逐项审查文件编辑，在更改到达时接受或拒绝，并发送后续提示来扩展工作，同时保留原有上下文。

本课介绍了以下内容：

- 实时监控智能体工作。
- 接受或拒绝单项文件编辑。
- 在会话进行中使用后续提示引导智能体。

接下来，在[下一课][next-lesson]发布无障碍工作并审查本地自定义智能体生成的更改。

## 资源

- [VS Code 中的 Copilot Chat][copilot-chat-vscode]
- [使用智能体模式][agent-mode]

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
