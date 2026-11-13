---
title: "练习 0：先决条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

开始 Copilot cloud agent 练习前，需要先做好准备。你将创建 Tailspin Toys 存储库的副本，并启动一个 [codespace][codespaces]，用来编辑指令文件和审查 cloud agent 生成的工作。

## 设置实验用存储库

要为练习中的代码创建存储库副本，请从[模板存储库][template-repository]创建一个实例。新实例包含实验所需的全部文件，后续练习都会用到它。

1. 在新的浏览器窗口中打开 [Tailspin Toys 模板][tailspin-template]。
2. 在实验存储库页面中选择 **Use this template** 按钮，然后选择 **Create a new repository**，创建存储库副本。

    ![Use this template 按钮](../../../_images/ex0-use-template.png)

3. 如果你正在参加由 GitHub 或 Microsoft 举办的讲师指导型活动，请遵循导师提供的说明。否则，可以在你有权使用 GitHub Copilot 的组织中创建新存储库。

    ![存储库模板设置输入界面](../../../_images/ex0-repository-settings.png)

4. 记下新存储库的路径（**organization-or-user-name/repository-name**），稍后会用到。

## 创建 codespace

接下来，你将使用 codespace 完成本实验中的练习。

[GitHub Codespaces][codespaces] 是云端开发环境，可让你直接在浏览器中编写、运行和调试代码。它提供功能完整的 IDE，支持多种编程语言、扩展和工具。

1. 打开刚创建的存储库。
2. 选择绿色的 **Code** 按钮。

    ![选择 Code 按钮](../../../_images/ex0-code-button.png)

3. 选择 **Codespaces** 选项卡，然后选择 **+** 按钮创建新的 Codespace。

    ![创建新的 codespace](../../../_images/ex0-create-codespace.png)

创建 codespace 需要几分钟，不过仍比手动安装所有服务快得多。等待期间，可以探索 GitHub Copilot 的其他功能，接下来会介绍这些功能。

> [!CAUTION]
> 后续练习还会回到这个 codespace。目前请在浏览器标签页中保持打开。

> [!NOTE]
> 本研讨会支持在 codespace 或本地 [dev container][dev-containers] 中运行。两者都预先安装了顺利完成练习所需的依赖项。如果想在本地运行，请在 VS Code 中打开克隆的存储库，并在提示时选择 **Reopen in Container**。VS Code 将构建与 codespace 相同的开发容器。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## 总结

恭喜，你已创建实验用存储库副本，并启动了 codespace。后续练习会在其中与 Copilot cloud agent 协同工作。

## 下一步

接下来，为 cloud agent 添加自定义指令。继续学习[练习 1：自定义指令][next-lesson]。

## 资源

- [GitHub Codespaces 概述][codespaces]
- [从模板创建存储库][template-repository]
- [开始使用 Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
