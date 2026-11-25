---
title: "练习 0：先决条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

开始 VS Code 练习前，需要准备好环境。你将创建 Tailspin Toys 存储库自己的副本、启动可在编辑器中使用的 [Codespace][codespaces]，并确认 GitHub Copilot Chat 已正常运行。

## 设置实验存储库

要创建用于编写代码的存储库副本，请基于[模板][template-repository]创建实例。新实例包含实验所需的全部文件，后续练习都会使用它。

1. 在新浏览器窗口中打开 [Tailspin Toys 模板][tailspin-template]。
2. 在实验存储库页面选择 **Use this template**，然后选择 **Create a new repository**。

   ![Use this template 按钮](../../../_images/ex0-use-template.png)

3. 如果此工作坊由 GitHub 或 Microsoft 的导师组织开展，请遵循导师提供的说明。否则，请在你有权使用 GitHub Copilot 的组织中创建新存储库。

   ![输入存储库模板设置](../../../_images/ex0-repository-settings.png)

4. 记下创建的存储库路径（**organization-or-user-name/repository-name**），后续实验会用到。

> [!NOTE]
> **待办事项已准备好**
>
> 从模板创建存储库时，会自动创建 GitHub issues 待办事项。整个工作坊都将使用这些议题，无需自行创建。

## 创建 Codespace

接下来使用 Codespace 完成实验练习。

[GitHub Codespaces][codespaces] 是基于云的开发环境，可直接在浏览器中编写、运行和调试代码。它是功能完整的 IDE，并支持多种编程语言、扩展和工具。

1. 打开新创建的存储库。
2. 选择绿色的 **Code** 按钮。

   ![选择 Code 按钮](../../../_images/ex0-code-button.png)

3. 选择 **Codespaces** 选项卡，再选择 **+** 按钮创建新 Codespace。

   ![创建新 Codespace](../../../_images/ex0-create-codespace.png)

Codespace 创建可能需要几分钟，但仍比手动安装所有服务快得多。

> [!CAUTION]
> 后续练习会返回此 Codespace。当前请将浏览器标签页保持打开。

> [!NOTE]
> 本工作坊可在 Codespace 或本地 [dev container][dev-containers] 中运行。两者都会确保环境具备所需前置条件。如果希望本地运行，请在 VS Code 中打开克隆的存储库，并在提示时选择 **Reopen in Container**。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## 使用 GitHub Copilot Chat 和智能体模式

要使用 GitHub Copilot Chat 智能体模式，需要在 IDE 中安装 GitHub Copilot Chat 扩展。如果使用 GitHub Codespace，通常已经安装。

> [!TIP]
> 如果尚未安装，可以从 [Visual Studio Code Marketplace][copilot-chat-extension] 安装 GitHub Copilot Chat。也可打开扩展视图，搜索 **GitHub Copilot Chat**并选择 **Install**。

安装扩展后，可能需要使用 GitHub 账户登录：

1. 返回 Codespace。
2. 如果编辑器右侧未显示 Copilot Chat，请选择 Codespace 顶部的 **Copilot Chat** 图标。
3. 在 Copilot Chat 窗口输入 `Hello world`并按 <kbd>Enter</kbd>。
4. 如果尚未认证，请按提示登录 GitHub。

   ![Copilot Chat 登录提示示例](../../../_images/ex1-copilot-authentication.png)

5. 登录后应能看到 Copilot Chat 窗口。

## 总结

恭喜，你已创建实验存储库副本！你也开始创建 Codespace，稍后将在其中编写代码。

## 下一步

现在让 Copilot 开始工作。继续学习[练习 1：自定义指令][next-lesson]，了解如何让 Copilot 遵循项目约定。

## 资源

- [GitHub Codespaces 概述][codespaces]
- [从模板创建存储库][template-repository]
- [开始使用 Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
