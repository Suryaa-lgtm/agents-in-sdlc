---
title: "练习 3 - 自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

[GitHub Copilot 中的自定义智能体][custom-agents-concept]可针对开发工作流中的特定任务或领域创建专业 AI 助手。通过在存储库的 `.github/agents` 文件夹中使用 Markdown 文件定义智能体，可为 Copilot 提供集中指令、最佳实践、编码模式和领域知识，引导它更有效地完成特定类型的工作。团队可将专业知识编码为可复用智能体，例如执行 [WCAG][wcag] 合规性的无障碍智能体、遵循安全编码实践的安全智能体，或维护一致测试模式的测试智能体。

自定义智能体由项目 `.github/agents` 文件夹中的 Markdown 文件或全局 `~/.copilot/agents` 中的 Markdown 文件定义。每个文件的 YAML frontmatter 至少包含 `name` 和 `description`，后面是定义智能体行为、专业知识和指令的 Markdown 提示词。

### 自定义智能体与智能体技能

自定义智能体和[智能体技能][agent-skills-concept]在逻辑上有一定重叠。两者主要都使用 Markdown 文件来指导 AI 执行操作。最清晰的区分是：**自定义智能体是执行者，技能是工具**。

自定义智能体拥有独立上下文窗口，可在完成工作时编排技能乃至其他智能体。本实验中的无障碍自定义智能体会依据无障碍指南审查并更新网站，并可在此过程中调用拉取请求工作流技能或运行和管理测试的技能。

> [!NOTE]
> 编写自定义智能体没有唯一正确方式。与所有 AI 工作一样，应通过测试和迭代找到适合环境与场景的方法。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

你将通过自定义智能体探索：

- 如何定义自定义智能体。
- 如何将任务分配给自定义智能体。

## 场景

Tailspin Toys 致力于确保其众筹平台对所有用户（无论视觉能力或偏好如何）均可访问。最近的反馈表明，一些用户因文本与背景色对比度不足而觉得当前深色主题难以阅读。为解决这一无障碍问题，设计团队要求实现可由用户打开或关闭的高对比度模式。

由于无障碍性至关重要，应尽快实现该功能。下面将使用自定义智能体生成实现。

## 审查无障碍自定义智能体

存储库已预先创建无障碍自定义智能体。下面审查它的内容，了解它如何引导 Copilot。

返回 Codespace并审查该自定义智能体文件：

1. 打开 `.github/agents/accessibility.md`。
2. 注意包含 `name` 和 `description` 字段的 YAML frontmatter。

> [!CAUTION]
> 自定义智能体的 `name` 和 `description` frontmatter 是必需的。

3. 浏览后续部分，了解：
   - 生成无障碍网站代码时的核心职责。
   - 无障碍最佳实践。
   - HTML、CSS 和 JavaScript 代码示例。
   - 常见陷阱和错误列表。

## 创建并分配议题

Mission control 是当前环境中管理所有智能体的中央位置。你可以在此分配任务、监控任务，并重定向或补充指导。

1. 打开存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 创建议题。
5. 将 **Title** 设置为 `Add high contrast mode to website`。
6. 将 **Description** 设置为：

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot** 打开分配对话框。
9. 在自定义智能体列表中选择 **Accessibility agent**。

   ![Cloud agent 分配界面，其中已突出显示自定义智能体和 Accessibility](../../../_images/ex5-select-custom-agent.png)

10. 选择 **Assign**。
11. Copilot 会在后台处理任务。

## 总结与后续步骤

本课探索了 GitHub Copilot 中面向特定任务和领域的专业助手——[自定义智能体][custom-agents]。自定义智能体可将团队的专业知识和标准编码为可复用智能体，引导 Copilot 更有效地完成特定工作。

你探索了：

- 自定义智能体的定义方式。
- 如何将任务分配给自定义智能体。

当 Copilot 正在实现高对比度模式时，可以转而在 Mission Control 中[监控并引导智能体会话][next-lesson]。

## 资源

- [关于自定义智能体][custom-agents]
- [在组织中准备使用自定义智能体][org-custom-agents]
- [在企业中准备使用自定义智能体][enterprise-custom-agents]

| [← 上一课：GitHub Copilot cloud agent][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
