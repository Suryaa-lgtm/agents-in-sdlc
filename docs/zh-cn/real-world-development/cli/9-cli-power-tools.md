---
title: "第 9 课 - GitHub Copilot CLI 中的斜杠命令"
description: "探索用于管理上下文、选择模型、共享会话和可选 cloud delegation 的斜杠命令。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

与其他优秀的 CLI 工具一样，GitHub Copilot CLI 提供大量斜杠命令用于交互。这些命令会公开高级功能、后台信息和其他配置选项。你已经使用过 `/diff`、`/mcp`、`/skills`、`/agent` 和 `/pr` 等命令，现在继续探索其他实用命令。

本课将介绍如何：

- 使用 `/context` 和 `/compact` 探索 Copilot 如何管理对话上下文。
- 使用 `/model` 探索可用模型。
- 了解 `/share` 如何导出或共享会话。
- 探索用于并行工作、工作树和委托给 cloud agent 的可选命令。

## 场景

核心 CLI 工作流已完成。现在了解一些附加能力：管理上下文、切换模型、共享会话，以及可选择委托工作给 [Copilot cloud agent][about-cloud-agent]。

## 探索 Copilot CLI 上下文

处理较大或较复杂任务时，可能会触达模型的最大上下文窗口。Copilot CLI 会在需要时自动压缩对话；你也可使用斜杠命令检查或压缩上下文。

1. 返回 Codespace。如果尚未打开 Copilot CLI，请从存储库根目录启动。
2. 输入：

   ```plaintext
   /context
   ```

3. 查看模型、当前 token 用量，以及上下文如何划分为系统指令、工具、消息和空余空间。
4. 压缩对话：

   ```plaintext
   /compact
   ```

5. 再次输入 `/context`并比较结果。如果对话本身较短，变化可能不明显。

> [!NOTE]
> 上下文窗口填满时，Copilot CLI 会自动压缩上下文。如果希望自行选择压缩时机，请使用 `/compact`。切换到无关任务并希望获得全新对话时，请使用 `/clear` 或 `/new`。

## 选择模型

不同模型具有不同优势，开发人员也有不同偏好。Copilot CLI 可列出并选择你要使用的模型。

1. 输入：

   ```plaintext
   /model
   ```

2. 浏览可用模型和用量信息。
3. 保留当前模型、选择其他模型，或按 <kbd>Esc</kbd> 关闭列表。

## 共享会话

团队协作和分享经验有助于每个人改进 AI 工具的使用方式。`/share` 可将会话导出为 Markdown 或 HTML 文件、创建可共享链接，或发布 GitHub gist。

1. 输入 `/help` 并查看所安装版本中的 `/share` 选项。
2. 若要共享此会话，请选择适合需求的目标，例如使用 `/share file` 导出本地 Markdown 文件。
3. 向任何人发送或发布前，请先审查导出的内容。会话导出可能包含提示词、回答和项目详细信息。

发布链接或 gist 是可选操作。不要发布团队无意共享的存储库或对话内容。

## 可选：横向扩展或委托

核心工作坊已完成。Copilot CLI 还提供适用于较大任务的命令：

- `/fleet` 可将相互独立的子任务分配给多个子智能体并行运行。
- `/worktree` 可为独立任务创建隔离的 Git worktree。
- `/delegate` 可将任务发送给 Copilot cloud agent，由其异步工作并可能打开拉取请求。

这些命令属于可选操作，因为它们可能创建额外工作树或远程工作。在尝试前，请先启动一个范围明确的新任务，并通过正常工作流审查结果。如果希望深入了解异步智能体工作，请继续学习 [cloud agent 工作坊][cloud-workshop]。

## 总结与后续步骤

在 Copilot CLI 中使用斜杠命令，可配置工具、共享会话并查看后台状态。本课中，你：

- 使用 `/context` 和 `/compact` 探索了 Copilot 如何管理对话上下文。
- 使用 `/model` 浏览了可用模型。
- 了解了 `/share` 如何导出或共享会话。
- 探索了用于并行工作、工作树和委托给 cloud agent 的可选命令。

还有更多斜杠命令可供探索！现在通过[审查已学内容][next-lesson]和后续学习方向结束本次旅程。

## 资源

- [Copilot CLI 命令参考][cli-reference]
- [Copilot CLI 中的上下文管理][context-management]
- [关于 Copilot cloud agent][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
