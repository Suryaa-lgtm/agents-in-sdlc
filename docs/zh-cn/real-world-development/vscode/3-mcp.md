---
title: "练习 3 - 使用 Playwright MCP 服务器测试功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：智能体模式][previous-lesson] · [下一课：自定义智能体 →][next-lesson]

你刚刚使用智能体模式构建了筛选功能。打开拉取请求前，应确认它在浏览器中能够正常工作。无需亲自逐步操作应用，可连接 **Playwright MCP 服务器**，让 Copilot 驱动真实浏览器为你测试功能，然后发布分支并打开 PR。

本练习将介绍如何：

- 了解 Model Context Protocol (MCP) 是什么，以及 MCP 服务器如何通过新工具扩展 Copilot。
- 在工作区中添加 Playwright MCP 服务器。
- 请 Copilot 使用 Playwright MCP 服务器，在浏览器中手动测试筛选功能。
- 发布分支，并为筛选工作打开拉取请求。

## 什么是 Model Context Protocol (MCP)？

当智能体能够访问编辑器之外的资源时，它的能力会强大得多。MCP 是 Copilot 实现这一点的方式：这是智能体与外部工具和服务通信的一种标准方式。

![智能体模式内部工作原理示意图，展示其如何与上下文、LLM 和工具交互，其中包括 MCP 服务器和 VS Code 扩展提供的工具](../../../_images/ex1-mcp-diagram.png)

[Model Context Protocol (MCP)][mcp-blog-post] 为 AI 智能体提供了与外部工具和服务通信的方式。使用 MCP 后，AI 智能体可以实时与外部工具和服务通信，从而访问最新信息（使用资源）并代你执行操作（使用工具）。

这些工具和资源通过 MCP 服务器访问。MCP 服务器充当 AI 智能体与外部工具和服务之间的桥梁，负责管理智能体与外部工具（例如现有 API 或 NPM 包等本地工具）之间的通信。每个 MCP 服务器都代表 AI 智能体可以访问的一组工具和资源。

下面是两个常见的 MCP 服务器：

- **[GitHub MCP Server][github-mcp-server]**：提供一组用于管理 GitHub 存储库的 API。AI 智能体可以使用这些 API 创建新存储库、更新已有存储库，以及管理议题和拉取请求。
- **[Playwright MCP Server][playwright-mcp-server]**：使用 Playwright 提供浏览器自动化能力。AI 智能体可以用它浏览网页、填写表单和选择按钮。

还有许多其他 MCP 服务器可提供不同的工具和资源。GitHub 托管了 [MCP registry][mcp-registry]，用于帮助发现并参与生态系统建设。

> [!CAUTION]
> 应像对待项目中的其他依赖项一样审查 MCP 服务器。使用前，请仔细检查其源代码、验证发布者并考虑安全影响。只使用信任的 MCP 服务器，并谨慎授予其访问敏感资源或执行敏感操作的权限。

## 审查 MCP 配置

`.vscode/mcp.json` 文件用于配置当前 VS Code 工作区可用的 MCP 服务器。

1. 在 Codespace 中打开 `.vscode/mcp.json`。
2. 你应该能看到已经配置好的 `github` 服务器：

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

`github` 条目随项目模板提供，因此上一练习中 Copilot 能够读取待办议题。它使用[远程 GitHub MCP 服务器][remote-github-mcp-server]，无需在本地安装任何内容——VS Code 通过 HTTP 连接到该服务器，并在 Copilot 首次使用其工具时让你使用 GitHub 完成身份验证。

## 添加 Playwright MCP 服务器

现在添加第二个服务器。[Playwright MCP 服务器][playwright-mcp-server]会为 Copilot 提供可控的浏览器，正适合用来测试新功能。

1. 在 `.vscode/mcp.json` 中，与 `github` 并列添加 `playwright` 条目，使文件内容如下：

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. 保存文件。

与远程 `github` 服务器不同，`playwright` 是**本地**服务器：VS Code 会在你的计算机上运行 `npx @playwright/mcp@latest` 来启动它。`--headless` 标志指示 Playwright 在没有可见窗口的情况下运行浏览器；Codespace 中没有可显示浏览器的桌面，因此必须使用此设置。

> [!NOTE]
> Tailspin Toys 项目已在端到端测试中使用 Playwright，因此 Playwright 所需的浏览器通常已经安装。如果 Copilot 随后报告缺少浏览器，请让它运行 `npx playwright install chromium`，然后重试。

## 启动并信任服务器

VS Code 会**按需**启动 MCP 服务器：Copilot 首次需要服务器提供的工具时，VS Code 会启动服务器并询问你是否信任它。

1. 在 `.vscode/mcp.json` 中，`playwright` 条目上方会出现 **Start** 操作。选择它以立即启动服务器，并确认配置正确。
2. 如果 VS Code 询问是否信任服务器，请审查配置并选择信任，以便启动服务器。

手动启动是可选操作。如果跳过这一步，VS Code 会在下一步中 Copilot 首次需要相关工具时启动服务器，并询问你是否信任它。

## 测试筛选功能

[Playwright MCP 服务器][playwright-mcp-server]为 Copilot 提供可操作的真实浏览器。它可以打开页面、导航、应用筛选器并读取结果，然后向你总结观察到的情况。你无需离开对话亲自浏览应用，就能快速确认功能是否符合预期。

在底层，Playwright MCP 服务器使用页面的[无障碍树][playwright-mcp-server]而不是屏幕截图。这样，智能体可以根据带标签的结构化元素（按钮、链接和列表项）进行推理，与辅助技术的工作方式相同。因此，快速功能检查也可以顺便验证一些基础无障碍体验。

服务器已连接且应用正在运行时，请 Copilot 测试刚完成的筛选功能：

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

Copilot 会通过 Playwright MCP 服务器启动浏览器、逐步执行测试并报告观察结果。根据议题中的验收标准审查其总结；如果发现异常，请继续提问，或让它在打开拉取请求前修复代码。

> [!NOTE]
> 测试时，应用必须运行在 `http://localhost:4321`。如果开发服务器已停止，请在发送提示词前重新启动。如果 Copilot 首次使用 Playwright MCP 服务器时需要下载浏览器，而它报告浏览器缺失，请让它运行 `npx playwright install chromium`，然后重试。

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## 发布分支并创建拉取请求

确认功能正常后，就可以打开拉取请求 (PR)，让团队审查。第一步是发布 `filtering-vscode` 分支。

1. 在 Codespace 中打开 **Source Control** 面板，并审查 Copilot 所做的更改。
2. 选择 **+** 图标暂存更改。
3. 使用 **Sparkle** 按钮生成提交消息。

   ![显示 Copilot 所做更改的 Source Control 面板屏幕截图](../../../_images/ex3-source-control-changes.png)

4. 选择 **Publish**，将分支推送到存储库。

## 创建拉取请求

创建拉取请求有多种方式，包括使用 github.com 和 GitHub 命令行界面 (CLI)。不过，你已经在使用 GitHub Copilot，不如让它代为创建 PR！它可以找到相关议题并创建与议题关联的 PR。

1. 打开 Copilot Chat 面板，选择 **New Chat** 开始新会话。
2. 在智能体下拉列表中选择 **Agent**，确保 Copilot 可以使用 GitHub 工具。
3. 请 Copilot 创建 PR：

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. 根据需要选择 **Continue**，允许 Copilot 执行收集信息和操作所需的任务。首次使用 GitHub 工具时，系统可能会要求你向 GitHub 进行身份验证；按提示完成操作即可。
5. 观察 Copilot 如何搜索议题、找到正确议题并创建 PR。
6. 选择 Copilot 生成的链接审查拉取请求，但**暂时不要合并**。

## 总结与后续步骤

恭喜！本练习中你：

- 了解了 Model Context Protocol (MCP) 是什么，以及 MCP 服务器如何通过新工具扩展 Copilot。
- 在工作区中添加了 Playwright MCP 服务器。
- 使用它在浏览器中手动测试筛选功能，然后再交付。
- 发布了分支，并为筛选工作打开了拉取请求。

你使用 MCP 服务器**测试**了一项功能，但 MCP 只是扩展 Copilot 的一种方式。接下来，[创建自定义智能体][next-lesson]，以简化无障碍审查等专门任务。

## 资源

- [MCP 是什么，为什么大家都在讨论它？][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [GitHub MCP Server][github-mcp-server]
- [GitHub MCP Registry][mcp-registry]
- [VS Code 中的 MCP 服务器][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
