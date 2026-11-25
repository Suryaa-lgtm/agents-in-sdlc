---
title: "练习 1 - 自定义指令（Cloud agent）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：Copilot cloud agent →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务需要以特定方式完成，或者 Copilot 应了解背景信息，就应确保这些上下文可被使用。[指令文件][instruction-files]正是用于提供此类指导，让 Copilot 不仅了解要做什么，还了解如何做。

本练习将介绍如何：

- 了解项目上下文、编码指南和文档标准如何通过存储库自定义指令和路径范围指令文件传递给 Copilot。
- 在 `.github/copilot-instructions.md` 中添加新的存储库级标准。

> [!NOTE]
> 与 VS Code 和 CLI 学习路径不同，这里不会进行前后对比提示：Copilot cloud agent 会在 GitHub issues 上异步工作，因此实时并排展示影响较困难。后续审查 cloud agent 创建的拉取请求时，可以观察指令文件的作用。

## 指令文件

### 场景

作为优秀的开发团队，Tailspin Toys 针对开发实践制定了一组准则和要求，包括：

- 数据层始终需要单元测试。
- UI 应采用深色模式并具有现代感。
- 应通过 TSDoc 文档注释在代码中添加文档。
- 应在每个文件头部添加注释块，说明文件用途。

通过指令文件，可确保 Copilot 获得正确的信息，并按照上述实践完成任务。

### 自定义指令

自定义指令可向 Copilot 提供上下文和偏好，帮助它理解编码风格与要求。你可以指定首选约定、库，甚至希望代码包含的注释类型。指令可面向整个存储库，也可面向特定文件类型以提供任务级上下文。

指令文件分为两类：

- `.github/copilot-instructions.md`：每次针对存储库的请求都会发送给 Copilot 的单个指令文件，包含适用于大多数聊天或 CLI 请求的项目级信息，例如技术栈、构建目标、最佳实践和全局指导。
- `.github/instructions/*.instructions.md`：可针对特定任务或文件类型创建，例如特定语言（TypeScript 或 Astro）、UI 组件或新单元测试集。

> [!NOTE]
> 在 IDE 中，指令文件仅用于 Copilot Chat 的代码生成，不用于代码补全或下一编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot cloud agent 在生成代码时都会使用存储库级指令和带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> 此外，Copilot 还支持使用其他标准的指令文件，包括 AGENTS.md 和 CLAUDE.md。

### 管理指令文件的最佳实践

- 将项目级指导集中放在 `copilot-instructions.md` 中，例如构建目标、项目结构和全局编码标准。
- 使用 `*.instructions.md` 为特定文件类型（单元测试、Astro 组件、数据层）或任务提供明确指令。
- 使用自然语言，保持指导清晰，并提供代码应有或不应有的示例。

创建指令文件没有唯一标准，就像使用 AI 没有唯一方式一样。通过实验可以找到最适合项目的方法。

> [!TIP]
> 使用 GitHub Copilot 的每个项目都应维护完善的指令文件集合。本项目包含用于 [UI 更新][ui-instructions]和 [Astro][astro-instructions]等任务的指令。
>
> Copilot 也可帮助生成指令文件。每个界面使用方式不同，例如 VS Code 中是 **Configure Chat → Generate Agent Instructions**，Copilot CLI 中是 `/init`。
>
> 若要寻找模板或起点，请查看 [awesome-copilot][awesome-copilot]，其中包含大量指令文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 探索项目中的自定义指令文件

花点时间阅读此存储库附带的指令文件：一个核心 `copilot-instructions.md`，以及面向各类任务的 `*.instructions.md` 文件集合。可在编辑器或 GitHub Web UI 中打开它们。

1. 打开 `.github/copilot-instructions.md`。
2. 浏览该文件，注意项目简介以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。在 **Code standards** 中查看嵌套的 **GitHub Actions Workflows** 指导。这些内容适用于所有 Copilot 交互。
3. 打开 `.github/instructions` 文件夹。注意其中包含 Astro 文件、Drizzle 数据层、测试等方面的指令。
4. 打开 `.github/instructions/unit-tests.instructions.md`。注意顶部的 `applyTo` 字段，它设置相对存储库根目录的 glob，用于确定指令适用的文件；这里会匹配 `**/*.test.ts` 等任何 TypeScript 测试文件。
5. 查看为此项目创建单元测试所需的具体指令。
6. 最后打开 `.github/instructions/drizzle.instructions.md` 并滚动到底部。注意其中指向其他指令文件（如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将较大的指令集拆分为较小的可复用文件，并让 Copilot 在生成代码时参考示例；其中的路径相对于指令文件，而不是存储库根目录。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分记录了项目编码标准，但尚未要求代码内文档。下一步你将添加 TSDoc 文档注释和文件注释头规则。

## 添加新的存储库标准

下一步是本练习唯一的编辑操作：添加项目级规则，要求文档以 TSDoc 注释和文件级注释头的形式存在于代码中。cloud agent 在后续处理分配的议题时会读取并遵循这些规则。

先创建分支：

1. 在 Codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。下面确保存储库编码标准已被清晰记录，以改善代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到约第 27 行附近的 **Code formatting requirements** 部分。该部分记录了项目编码标准，但尚未要求代码内文档，这就是生成的辅助代码缺少文档注释的原因。
3. 在现有标准下方添加以下 Markdown：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 指令文件可在存储库级别（`.github/copilot-instructions.md`）提供全局指导，也可作为 `*.instructions.md` 面向特定语言、文件类型或任务。对于刚添加的文档注释规则，存储库级文件是合适的位置。

## 提交、推送并合并指令更新

Cloud agent 会读取议题目标分支中的指令文件。下一个练习将议题分配给 Copilot 时，Copilot 会从 `main` 创建分支，因此指令更改必须进入 `main`。

1. 暂存并提交：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 到 `main` 的拉取请求并合并。下一个练习分配议题后，cloud agent 就会读取这些指令。

> [!TIP]
> 如果本工作坊希望直接在 `main` 上工作，也可以跳过分支并直接提交。保留分支步骤可让工作坊更贴近真实项目流程。

## 总结与后续步骤

你探索了 Copilot 如何从本项目的指令文件获取上下文，并在 `.github/copilot-instructions.md` 中添加了新的存储库级标准。本学习路径剩余部分会在 cloud agent 创建的拉取请求中观察该标准的实际效果。

接下来，[将第一个议题分配给 Copilot cloud agent][next-lesson]。

## 资源

- [用于 GitHub Copilot 自定义的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot：指令文件及其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
