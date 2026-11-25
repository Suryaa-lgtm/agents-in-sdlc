---
title: "第 7 课 - 创建并使用 QA 智能体"
description: "创建一个 QA 自定义智能体，将议题要求、quality-checks 技能和 Playwright MCP 结合起来。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

你已使用 `quality-checks` 技能运行自动检查，并使用 Playwright MCP 在浏览器中观察筛选体验。现在，将这些能力整合到一个流程明确的自定义智能体中。

本课将介绍如何：

- 探索自定义智能体如何配合指令、技能和 MCP 工具工作。
- 创建并检查可复用的质量保证配置。
- 选择 QA 智能体，并对照筛选议题审查其发现。

## 场景

Tailspin Toys 希望在打开拉取请求 (PR) 前，对需求、代码质量、自动检查、测试覆盖率和浏览器行为进行一致审查。自定义智能体可协调这一 QA 流程并生成可复用报告。

## 什么是自定义智能体？

自定义智能体是在 Markdown 配置中定义的、具有专门用途的 Copilot 版本。配置描述智能体的用途、指令和可用工具。本工作坊将在 `.github/agents/qa.agent.md` 中定义 QA 角色，并在 Copilot CLI 中选择它。

此前使用的自定义功能各司其职：存储库指令描述团队标准，`quality-checks` 技能打包可重复执行的检查，Playwright MCP 提供浏览器工具，QA 配置则告诉 Copilot 如何利用这些能力评估需求并报告发现。它不会取代这些能力，也不需要另一个对话。

## 创建 QA 配置

在打开功能 PR 前，请 Copilot 创建可复用的 QA 配置。该配置将定义 QA 执行的检查及其必须遵守的边界。

1. 返回 Codespace，并确认筛选对话处于 Interactive 模式。
2. 请默认智能体创建新的自定义智能体：

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## 检查配置

使用新智能体前，请审查其配置，确认 Copilot 已捕获预期的 QA 工作流和边界。这样可以避免不完整或范围过大的智能体在你只想验证功能时修改实现。

1. 输入 `/diff` 并打开 `.github/agents/qa.agent.md`。
2. 阅读 frontmatter。`description` 是必需的；`name` 可选，但加入后可为智能体提供清晰的显示名称。
3. 阅读配置指令，确认 QA 从需求出发、遵循存储库指令、运行 `quality-checks` 技能，并使用 Playwright MCP。
4. 确认 QA 会提供证据、修改实现代码前先询问，并且不会提交更改或打开拉取请求。
5. 如果生成的配置遗漏了任何职责或边界，请在继续前让默认智能体修改。

## 针对议题运行 QA

Copilot CLI 在对话开始时加载项目智能体。创建配置后恢复同一个筛选对话，再选择 QA，以便它使用已在上下文中的议题和规划决定。

1. 使用以下提示词启用智能体：

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 刚创建智能体时，它可能不会出现在可用智能体列表中，但它已经存在，上述命令会激活它。

2. 使用以下提示词，请 QA 智能体审查功能：

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA 智能体开始工作。
4. 完成后阅读它提供的报告。

## 总结与后续步骤

你已为工作流添加可复用的专业角色，并审查了它的工作。本课中，你：

- 探索了自定义智能体如何配合指令、技能和 MCP 工具工作。
- 创建并检查了可复用的质量保证配置。
- 选择了 QA 智能体，并对照筛选议题审查了其发现。

现在，实现、技能更新、QA 配置、测试和验证报告均已准备好接受审查。接下来，你将[将它们整合到功能 PR 中并使用 Agent Merge][next-lesson]。

## 资源

- [为 Copilot CLI 创建自定义智能体][create-agents]
- [自定义智能体配置][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
