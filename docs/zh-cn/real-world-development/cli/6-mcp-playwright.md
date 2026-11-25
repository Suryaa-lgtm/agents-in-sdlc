---
title: "第 6 课 - 使用 Playwright MCP 验证功能"
description: "在 Copilot CLI 中检查或配置 Playwright MCP，并使用浏览器探索筛选功能。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

编写代码并不是软件开发的全部。我们还需要处理数据、使用外部服务，并让 Copilot 能够调用其他自动化工具。这正是 MCP 服务器发挥作用的地方。MCP 服务器让 Copilot 能够超越 CLI 内置能力，使用更多工具和服务。

本课将介绍如何：

- 理解 Model Context Protocol (MCP) 是什么，以及 Copilot CLI 如何使用它。
- 未配置时添加 Playwright MCP 服务器。
- 请智能体驱动浏览器并探索筛选功能。

## 场景

单元测试和端到端测试虽然重要，但验证 UI 更新时仍需实际与界面交互。你希望让 Copilot 以用户的方式使用网站，以进一步自动化更改验证并提高更新符合预期的信心。

## 什么是 Model Context Protocol (MCP)？

[Model Context Protocol (MCP)][mcp-blog-post]让 AI 智能体能够与外部工具和服务通信。通过 MCP，AI 智能体可以实时与外部工具和服务通信，以访问最新信息并代你执行操作。

这些工具和资源通过 MCP 服务器访问。MCP 服务器充当 AI 智能体与外部工具和服务之间的桥梁。每个 MCP 服务器代表 AI 智能体可以访问的一组不同工具或资源。

常见的 MCP 服务器包括：

- **[GitHub MCP Server][github-mcp]**：提供管理 GitHub 存储库、议题和拉取请求所需的 API。
- **[Playwright MCP Server][playwright-mcp-server]**：使用 Playwright 提供浏览器自动化能力。

GitHub 托管的 [MCP registry][mcp-registry] 可帮助发现和贡献生态系统中的其他 MCP 服务器。

> [!CAUTION]
> MCP 服务器应按项目中的其他依赖项对待。使用前请审查源代码、验证发布者，并考虑安全影响。

## 添加 Playwright MCP 服务器

如果尚未配置 Playwright MCP 服务器，请添加它，让 Copilot 能像用户一样与网站交互。

> [!NOTE]
> 如果 Copilot CLI 已配置 Playwright MCP，请跳过以下设置步骤并继续下一节。

1. 返回 Codespace。
2. 在 Copilot CLI 中输入以下命令打开 MCP 服务器添加对话框：

   ```plaintext
   /mcp add
   ```

3. 名称输入 `playwright`，然后按 <kbd>Tab</kbd>。
4. 按 <kbd>Enter</kbd> 确认服务器类型为 **STDIO**，再按 <kbd>Tab</kbd>。
5. 在 **Command** 对话框中粘贴：

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. 按 <kbd>Control</kbd>+<kbd>S</kbd> (Mac) 或 <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) 保存新 MCP 服务器。
7. 按 <kbd>Esc</kbd> 退出 MCP 对话框。

## 请 Copilot 通过 Playwright 探索功能

此前你已手动确认功能符合预期。现在使用 Copilot 提供的 Playwright MCP 服务器执行相同验证。

1. 使用以下提示词让 Copilot 使用 Playwright MCP 验证功能：

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> Copilot 通常会自行判断并使用 MCP 服务器，因此并非必须明确要求。但由于你知道应使用的工具，主动指出方向不会有坏处，还可以提高结果一致性并节省 token。

2. 观察 Copilot 列出浏览器中执行的各项步骤，以确认功能正常。
3. 阅读报告并确认一切符合预期。

Copilot 会启动服务器、使用 Playwright 与网站交互、停止服务器，并向你提供报告。

## 总结与后续步骤

你已在 Copilot CLI 中使用 Playwright MCP，从真实浏览器探索功能。回顾一下，你：

- 了解了 Model Context Protocol (MCP) 以及 Copilot CLI 如何使用它。
- 在尚未配置时添加了 Playwright MCP 服务器。
- 请智能体驱动浏览器并探索筛选功能。

接下来，你将[创建 QA 自定义智能体][next-lesson]，把技能和浏览器工具整合到专业角色中。

## 资源

- [MCP 是什么，为什么大家都在讨论它？][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [为 Copilot CLI 添加 MCP 服务器][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
