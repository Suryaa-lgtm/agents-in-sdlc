---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

在前几个练习中，你请 Copilot cloud agent 完成了三项独立任务，目标是改善用户体验并添加功能。虽然 cloud agent 可异步自主运行，但监控这些任务仍然很重要。

GitHub.com 上的[智能体页面][agents-page]等工具可帮助你管理分配给 cloud agent 的任务。在此 Mission Control 中，可查看所有具有开放拉取请求的智能体任务；可检查已执行的操作，甚至在会话进行时进行引导。

本课将介绍如何：

- 浏览智能体页面以监控 cloud agent 任务。
- 引导进行中的会话并请求附加功能。

## 场景

分配智能体创建高对比度模式后，团队认为此时也应添加浅色模式。既然已有工作用于更新网站样式并添加切换功能，再加入浅色模式是合理的。你希望引导智能体，同时添加浅色模式和高对比度模式。

## 查看 Copilot cloud agent 任务

查看分配给 Copilot cloud agent 的所有任务的当前状态。

1. 打开 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主窗格和左侧窗格中的任务列表。应能看到已分配给 Copilot 的任务，包括：
   - 更新代码库文档。
   - 生成用于修改游戏的 API。
   - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，审查 Copilot 已执行的步骤，例如：
   - 从存储库检出代码。
   - 为 Copilot 创建环境。
   - 设置 MCP 服务器。
   - 执行完成任务所需的各项步骤。

> [!NOTE]
> 列出的具体步骤会根据 Copilot 的工作状态和采用的方法而有所不同。

4. 注意右侧出现的拉取请求 (PR) 窗格，可在其中查看 PR 和已更改文件以进行进一步监控。

## 引导 cloud agent

既然已看到当前活跃任务，下面请 Copilot 在处理高对比度模式时一并添加浅色模式切换。

1. 选择与添加高对比度模式相关的会话。准确标题会因 Copilot 使用的名称及当前工作状态而异。

   ![Mission Control 中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 查看会话几分钟，直到它表示已完成设置并开始工作。当看到类似以下的消息时，即表示已进入此状态。
3. 在 **Steer active session while Copilot is working** 对话框中输入：

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![智能体页面中的 cloud agent 任务，已突出显示 steer active session while copilot is working 对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd>发送提示词。
5. 注意 Copilot 如何确认提示词，并将其纳入工作流程。

## 让 Copilot 完成工作

与之前一样，Copilot 会处理更新后的任务。发送消息后，它会在完成当前步骤后将新要求纳入流程。

任务仍需几分钟完成，可以借此暂停并回顾目前学到和探索的内容。

## 总结与后续步骤

本课探索了 Copilot 智能体页面，即监控和引导 GitHub Copilot cloud agent 任务的中央中心。通过 Mission Control，可跟踪活跃和已完成的任务、审查正在执行的工作，甚至重定向进行中的任务以调整范围或补充指导。

你探索了：

- 使用 Mission Control 和智能体页面监控 cloud agent 任务。
- 重定向进行中的会话以请求附加功能。

当 Copilot 完成无障碍功能时，可转而[迭代 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
