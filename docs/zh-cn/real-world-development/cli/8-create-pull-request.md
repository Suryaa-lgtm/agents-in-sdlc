---
title: "第 8 课 - 创建并合并功能 PR"
description: "集中审查筛选功能、指令、技能更新、QA 配置和测试，然后创建 PR 并使用 Agent Merge。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

筛选实现、指令更新、技能更新、质量保证 (QA) 配置和测试均已保存在同一个分支上。现在集中审查这些更改并创建拉取请求。星级评分 PR 是你亲自合并的；这次将允许 **Agent Merge** 管理合并流程。

> [!NOTE]
> 通常会将功能、指令更新、技能更新和 QA 智能体拆分成多个 PR。为简化工作坊，你在同一个对话和分支中完成筛选与质量工作流，并将全部更改纳入此 PR。

本课将介绍如何：

- 了解 Agent Merge 是什么，以及它如何自动化合并生命周期。
- 检查完整功能更改和验证证据。
- 创建筛选功能 PR。
- 在审查后启用 Agent Merge，并确认 PR 已合并。

## 场景

在筛选工作流中，你使用 Copilot 规划、实现并验证功能。Tailspin Toys 希望自动化剩余 PR 工作，同时将合并授权留给开发人员控制。

## Agent Merge 简介

**Agent Merge** 可自动化交付拉取请求所需的剩余工作。启用后，Copilot 会处理阻止 PR 的因素，例如修复失败的持续集成 (CI) 棪查、回应审查评论，以及需要时 rebase，然后在存储库允许时启用 GitHub 自动合并。

此前你会亲自选择 **Merge pull request**。现在可以由 Agent Merge 接手此职责，但应先审查工作并确认已准备就绪，再启用 Agent Merge。

## 使用 Agent Merge 管理 PR

所有代码都已创建，现在集中审查、创建 PR，并让 Agent Merge 管理后续流程。

1. 返回 Codespace。
2. 输入 `/agent` 打开智能体对话框。
3. 在选项列表中选择 **Default**，再按 <kbd>Enter</kbd>。
4. 输入 `/pr create` 创建新 PR。
5. 输入 `/pr agentmerge` 激活 Agent Merge。
6. Copilot 会监视 PR 上的持续集成流程。全部成功后，它会执行合并。
7. 确认看到类似 “PR #14 was squash-merged successfully.” 的 Copilot 消息。

> [!IMPORTANT]
> Agent Merge 不会绕过必需批准、分支保护、合并队列、存储库设置或权限不足。如果流程受阻，请阅读报告原因，并在存储库允许时手动完成已审查的合并。

## 总结与后续步骤

你已自动化开发流程中的多个环节，包括生成代码、测试和验证代码，以及拉取请求流程。具体而言，你：

- 了解了 Agent Merge 是什么，以及它如何自动化合并生命周期。
- 检查了完整功能更改和验证证据。
- 创建了筛选功能 PR。
- 在审查后启用了 Agent Merge，并确认 PR 已合并。

接下来，你将[探索更多有用的 Copilot CLI 斜杠命令][next-lesson]，了解上下文、模型、共享及可选的 cloud delegation。

## 资源

- [使用 Copilot CLI 管理拉取请求][manage-prs]
- [Copilot CLI 命令参考][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
