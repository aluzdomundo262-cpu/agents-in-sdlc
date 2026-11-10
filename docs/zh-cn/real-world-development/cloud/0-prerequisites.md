---
title: "练习 0：先决条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

开始 Copilot 云智能体练习前，请先做好准备。你将从模板创建自己的 Tailspin Toys 存储库副本，并启动一个 [Codespace][codespaces]，用于编辑指令文件和审查云智能体的工作成果。

## 设置实验存储库

先从[模板存储库][template-repository]创建项目副本。该存储库包含实验所需的全部文件，后续练习都会使用它。

1. 在新的浏览器窗口中，打开 [Tailspin Toys 模板][tailspin-template]。
2. 在实验存储库页面选择 **Use this template**，然后选择 **Create a new repository**，创建自己的存储库副本。

    ![Use this template 按钮](../../../_images/ex0-use-template.png)

3. 如果你是在 GitHub 或 Microsoft 主办的活动中参加本工作坊，请遵循导师提供的说明。否则，可在你有权使用 GitHub Copilot 的组织中创建新存储库。

    ![存储库模板设置输入界面](../../../_images/ex0-repository-settings.png)

4. 记下所创建的存储库路径 (**organization-or-user-name/repository-name**)，后续练习会用到它。

## 创建 Codespace

接下来使用 Codespace 完成本实验的练习。

[GitHub Codespaces][codespaces] 是云端开发环境，可让你直接在浏览器中编写、运行和调试代码。它是功能齐全的集成开发环境 (IDE)，支持多种编程语言、扩展和工具。

1. 打开刚创建的存储库。
2. 选择绿色的 **Code** 按钮。

    ![选择 Code 按钮](../../../_images/ex0-code-button.png)

3. 选择 **Codespaces** 选项卡，然后选择 **+** 按钮创建新的 Codespace。

    ![创建新的 Codespace](../../../_images/ex0-create-codespace.png)

Codespace 可能需要几分钟才能创建完成，不过这仍比手动安装所有服务快得多。等待期间，可以先探索 GitHub Copilot 的其他功能，接下来会介绍相关内容。

> [!CAUTION]
> 后续练习还会用到这个 Codespace。现在先不要关闭它，请让它保持在浏览器标签页中。

> [!NOTE]
> 本工作坊可在 Codespace 或本地[开发容器][dev-containers]中运行。两者都会预装所需的先决条件。如果想在本地运行，请在 VS Code 中打开克隆的存储库，并在出现提示时选择 **Reopen in Container**。VS Code 将构建与 Codespace 相同的开发容器。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## 总结

恭喜，你已创建实验存储库副本，并开始创建 Codespace。后续练习中，你将在该环境中与 Copilot 云智能体协作。

## 下一步

接下来添加云智能体将遵循的自定义指令，继续[练习 1：自定义指令][next-lesson]。

## 资源

- [GitHub Codespaces 概述][codespaces]
- [从模板创建存储库][template-repository]
- [开始使用 Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
