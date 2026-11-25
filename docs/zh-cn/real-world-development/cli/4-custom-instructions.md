---
title: "第 4 课 - 使用自定义指令引导 Copilot"
description: "探索存储库指令，添加文档标准，并将其应用于筛选代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

使用生成式 AI 时，上下文至关重要。如果任务需要以特定方式完成，就应让 Copilot 获得相应指导。[指令文件][instruction-files]不仅说明需要什么代码，还说明代码应如何组织。筛选功能已经构建完成，现在你将探索 Copilot 使用的指令、添加文档标准，并将其应用于代码。

本课将介绍如何：

- 探索存储库指令和路径范围指令文件如何传递给智能体。
- 更新指令文件以确保遵循编码标准。
- 查看指令文件对代码的影响。

## 场景

作为优秀的开发团队，Tailspin Toys 为开发实践制定了一组准则和要求，包括：

- 注释应说明意图和不明显的决策，而不是复述代码。
- `db/` 和 `src/lib/` 中导出的函数应使用 TSDoc/JSDoc 记录用途、参数和返回值；如果存在可注入的 `db` 参数，也应记录。
- 可复用的 Astro 组件应记录其 `Props` 契约，并在相关代码变化时同步更新注释。
- 应保留现有格式和 lint 指导。

通过指令文件，可以确保 Copilot 获得正确的信息，并按照上述实践完成任务。

## 指令文件

自定义指令可向 Copilot 提供上下文和偏好，使其更好地理解编码风格与要求。你可以为整个存储库指定首选约定，也可以为特定文件类型提供任务级上下文。

指令文件分为两类：

- `.github/copilot-instructions.md`：每次针对存储库的请求都会发送给 Copilot 的单个指令文件，用于提供适用于大多数请求的项目级信息。
- `.github/instructions/*.instructions.md`：针对特定语言、文件类型或任务提供指导。

> [!NOTE]
> 其他指令格式及支持情况因环境而异。依赖特定格式前，请查阅[自定义指令支持参考][custom-instructions-support]。

## 探索项目中的自定义指令文件

初始项目已包含一组指令文件。进行更改前，先探索现有内容并了解它们的作用。

1. 返回 Codespace。
2. 在 Codespaces 编辑器中打开（不是终端）`.github/copilot-instructions.md`。
3. 浏览该文件，注意项目简介和编码指导。这些指令适用于该存储库中与 Copilot 的所有交互。
4. 打开 `.github/instructions` 文件夹并浏览其中的文件。你会看到针对 Astro 文件、Drizzle 数据层、测试等内容的指令。
5. 打开 `.github/instructions/unit-tests.instructions.md`。注意顶部的 `applyTo` 字段，它通过 glob 决定指令适用的文件。
6. 打开 `.github/instructions/drizzle.instructions.md`，并注意它指向其他指令文件和现有项目文件的链接。这样可将较大的指令集拆分为较小的可复用文件，并让 Copilot 参考示例。

## 更新指令文件以符合团队指导

现有文件是良好的起点，但仍有缺漏。下面修改核心的 `copilot-instructions.md` 文件，确保新生成的 TypeScript 添加 TSDoc 注释。

1. 在 `.github/copilot-instructions.md` 中找到标题为 **Code formatting guidance** 的部分，通常位于约第 35 行。
2. 将以下内容添加为最后一个列表项：

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

保存文件！

## 使用更新后的指导

Copilot CLI 在对话开始时加载存储库指令。保存更新后的指令后，退出并恢复筛选对话，使 Copilot 在保留功能上下文的同时采用新指导。

1. 如果筛选对话仍在运行，输入 `/exit` 将其关闭。Copilot CLI 会自动保存对话。
2. 在 `game-filters-cli` 分支的存储库根目录恢复已保存的对话：

   ```bash
   copilot --resume
   ```

   如出现提示，请选择筛选对话，并确认已检出 `game-filters-cli` 分支。
3. 请 Copilot 应用更新后的指导：

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. 输入 `/diff` 并阅读变更后的 TypeScript 文件。确认新生成的 TSDoc 注释准确解释了代码。

## 总结与后续步骤

你探索了 Copilot CLI 如何从指令文件获取上下文，并将新标准应用于功能。具体而言，你：

- 探索了存储库指令和路径范围指令文件如何传递给智能体。
- 更新了指令文件以确保遵循编码标准。
- 查看了指令文件对代码的影响。

接下来，你将[自定义并运行可复用的 quality-checks 技能][next-lesson]，确保持续运行 lint 和测试。

## 资源

- [为 Copilot CLI 添加自定义指令][instruction-files]
- [自定义指令支持][custom-instructions-support]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [Awesome Copilot — 指令文件及其他资源集合][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
