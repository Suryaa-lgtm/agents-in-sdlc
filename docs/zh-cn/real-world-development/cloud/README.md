---
slug: zh-cn/real-world-development/cloud
title: "GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

**[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** 让 GitHub Copilot 在云端异步工作。你在 GitHub 上分配任务，cloud agent 会在后台接收任务、探索存储库、进行更改并打开拉取请求，因此你可以专注于其他工作。

在这些练习中，你将添加 cloud agent 遵循的自定义指令，然后分配 GitHub issue，让它实现功能。你会审查并使用自定义智能体塑造工作方式，在智能体仪表板中监控和引导会话，最后审查拉取请求并迭代结果。

## 练习

| 练习 | 主题 | 说明 |
|----------|-------|-------------|
| [0. 先决条件][ex0] | 设置 | 创建存储库和 Codespace |
| [1. 自定义指令][ex1] | 上下文 | 添加 cloud agent 将遵循的自定义指令 |
| [2. Cloud Agent][ex2] | 异步智能体 | 将议题分配给 Copilot cloud agent |
| [3. 自定义智能体][ex3] | 专业智能体 | 审查并使用自定义智能体 |
| [4. 管理智能体][ex4] | 监控 | 监控并引导智能体会话 |
| [5. 迭代][ex5] | 审查 | 审查 PR、迭代 Copilot 的工作并选择后续步骤 |

## 先决条件

参加本工作坊前，请确保具备：

- [ ] 已启用 **Copilot Student、Pro、Pro+、Business 或 Enterprise** 计划的 GitHub 账户
- [ ] 已为账户或组织启用 Copilot cloud agent

> [!TIP]
> 没有付费计划？经过验证的学生可通过 [GitHub Education][callout-student-plan-education] 免费使用 GitHub Copilot。**Copilot Student** 计划包含本工作坊使用的智能体、MCP、代码审查和 Copilot CLI 功能，可完成所有学习路径。

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> Cloud agent 适用于 **Copilot Student、Pro、Pro+、Business 和 Enterprise**；除 Copilot Free 外均可使用。使用 Copilot Business 或 Enterprise 时，管理员必须为组织启用。

> [!NOTE]
> 本学习路径不涵盖 MCP。如需探索 Copilot 使用 MCP 服务器，请参阅 [CLI 学习路径](../cli/)或 [VS Code 学习路径](../vscode/)。

## 开始

**[从练习 0：先决条件开始 →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
