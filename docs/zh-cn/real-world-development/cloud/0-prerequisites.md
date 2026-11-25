---
title: "练习 0：先决条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

开始 Copilot cloud agent 练习前，需要完成环境准备。你将创建 Tailspin Toys 存储库自己的副本，并启动一个可用于编辑指令文件和审查 cloud agent 工作成果的 [Codespace][codespaces]。

## 设置实验存储库

要创建用于编写代码的存储库副本，请基于[模板][template-repository]创建实例。新实例包含实验所需的全部文件，后续练习都会使用它。

1. 在新的浏览器窗口中打开 [Tailspin Toys 模板][tailspin-template]。
2. 在实验存储库页面选择 **Use this template** 按钮，然后选择 **Create a new repository**。

    ![Use this template 按钮](../../../_images/ex0-use-template.png)

3. 如果本工作坊由 GitHub 或 Microsoft 的导师组织开展，请遵循导师提供的说明。否则，请在你有权使用 GitHub Copilot 的组织中创建新存储库。

    ![输入存储库模板设置](../../../_images/ex0-repository-settings.png)

4. 记下创建的存储库路径（**organization-or-user-name/repository-name**），后续实验会用到。

## 创建 Codespace

接下来使用 Codespace 完成实验练习。

[GitHub Codespaces][codespaces] 是基于云的开发环境，可直接在浏览器中编写、运行和调试代码。它是功能完整的 IDE，并支持多种编程语言、扩展和工具。

1. 打开新创建的存储库。
2. 选择绿色的 **Code** 按钮。

    ![选择 Code 按钮](../../../_images/ex0-code-button.png)

3. 选择 **Codespaces** 选项卡，再选择 **+** 按钮创建新 Codespace。

    ![创建新 Codespace](../../../_images/ex0-create-codespace.png)

Codespace 的创建可能需要几分钟，但仍比手动安装所有服务快得多。借此时间，你可以继续探索 GitHub Copilot 的其他功能。

> [!CAUTION]
> 你会在后续练习中返回此 Codespace。目前请将浏览器标签页保持打开。

> [!NOTE]
> 本工作坊可在 Codespace 或本地 [dev container][dev-containers] 中运行。两者都会确保环境具备流畅体验所需的全部前置条件。如果希望本地运行，请打开克隆的存储库，在 VS Code 中提示时选择 **Reopen in Container**；VS Code 会构建与 Codespace 相同的 dev container。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## 总结

恭喜，你已创建实验存储库副本，并开始创建 Codespace。后续工作会与你的 Copilot cloud agent 一起进行。

## 下一步

让我们添加 cloud agent 将遵循的自定义指令。继续学习[练习 1：自定义指令][next-lesson]。

## 资源

- [GitHub Codespaces 概述][codespaces]
- [从模板创建存储库][template-repository]
- [开始使用 Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
