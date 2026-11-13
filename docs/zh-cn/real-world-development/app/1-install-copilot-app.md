---
title: "第 1 课 - 安装 GitHub Copilot app"
description: "安装 GitHub Copilot app，连接通过模板创建的存储库，熟悉工作区并尝试快速聊天。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

**[GitHub Copilot app][about-copilot-app]** 是一款用于智能体驱动开发的桌面应用，基于 GitHub Copilot CLI 构建并与 GitHub 原生集成，因此存储库、分支和 CI 管道开箱即用。它面向由你指挥多个智能体并行工作的流程，每个智能体都在独立工作区中运行，而不是由你亲自完成所有工作；它还可以自动处理重复任务。安装好 Node.js 并准备好项目副本后，接下来安装应用并连接该存储库。

本课将：

- 安装 GitHub Copilot app 并登录。
- 从 GitHub 存储库将项目添加到应用。
- 熟悉工作区，包括模板为你创建的待办事项。
- 尝试快速聊天，了解应用本身。

## 场景

你的团队正在使用 AI 智能体处理不断增长的待办事项。Copilot app 提供统一的工作区来指挥这些工作，包括认领议题、运行智能体、审查更改和合并拉取请求。本课将指导你安装应用、连接项目，并开始针对项目进行对话。

> [!NOTE]
> 需要符合条件的 Copilot 计划：Copilot Free、Copilot Student 或任何付费计划（Pro、Pro+、Business 或 Enterprise）。如果使用 Copilot Business 或 Copilot Enterprise，管理员必须保持 **GitHub Copilot app** 策略启用。

## 安装并配置 GitHub Copilot app

要使用 GitHub Copilot app，首先需要安装应用。Windows、macOS 和 Linux 均提供相应版本。现在安装应用、完成身份验证，并将 Tailspin Toys 存储库添加到应用。

1. 在浏览器中打开 [GitHub Copilot app 主页][download-app]。
2. 下载适用于当前平台的应用，并按主页提供的说明安装。
3. 安装完成后打开应用。
4. 选择 **Sign in to GitHub** 并按提示完成身份验证。如果使用具有数据驻留功能的 GitHub Enterprise Cloud，请选择 **Use GitHub Enterprise**，并在提示时输入 `*.ghe.com` 主机名。GitHub Enterprise Server 不受支持。
5. 如果引导流程提供存储库选择，请选择从模板创建的 Tailspin Toys 存储库。也可以跳过存储库选择，并在完成引导后添加项目。
6. 如果系统提示，请选择主题并完成引导。
7. 在侧边栏的 **Sessions** 下查找存储库。如果已经列出，就无需再次添加。
8. 如果尚未连接存储库，请选择 **Sessions** 旁边的 **+** 创建新会话，然后选择 **Add GitHub repository**。输入先决条件课程中记录的所有者和存储库名称。
9. 确认存储库显示在侧边栏中。此处采用的界面布局会将 `tailspin-toys` 等存储库文件夹归在 **Sessions** 下，每个存储库下方列出单独的会话。

## 熟悉工作区

项目连接后，先熟悉应用。侧边栏中的几个区域用于组织工作：

- **New**：从此处开始与 Copilot 的新聊天会话。
- **Pull requests**：通过应用内置的 GitHub 集成查看拉取请求。可以浏览和筛选 PR、检查 CI 状态并审查 PR，无需离开应用。
- **Issues**：以相同方式查看议题。可以浏览和筛选议题，并从议题启动会话。
- **Automations**：保存按计划或按需运行的智能体任务。适合管理待办事项清单、定期项目维护或其他希望委托处理的繁琐工作。总结课程会将其作为后续探索内容，而非另一项研讨会练习。
- **Customize**：添加 MCP 服务器、插件、技能和其他组件，扩展 Copilot app 的功能。之后会在此处配置 Playwright MCP。
- **Chats**：用于提问和头脑风暴的轻量对话，无需专属分支或工作区。首次开始聊天后，此区域才会显示。如果未显示，请选择 **Sessions** 旁边的 **+**，开始第一次聊天。
- **Sessions**：按存储库文件夹组织智能体会话。选择存储库名称（例如 `tailspin-toys`）可打开存储库视图；选择存储库下方的会话可返回对应对话。每个会话都在独立工作区运行，因此可以同时运行多个会话且不会相互覆盖。添加星级评分时将启动第一个会话。

随着研讨会继续，你会逐步了解整个工作区！

> [!TIP]
> 不确定时，可以直接询问 Copilot！如果不清楚某项操作或是否可行，可以请 Copilot 帮忙指导。

### 查找预置的待办事项

几乎每个项目都有待办事项，Tailspin Toys 也不例外。现在查看创建模板时自动生成的待办事项。

1. 在侧边栏的 **Sessions** 下选择 Tailspin Toys 存储库文件夹（不要选择其下方的单个会话），然后在存储库顶部导航中选择 **Issues**。
2. 根据标题查找以下议题，不要假定它们的议题编号：

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. 选择议题并阅读详情。每个议题也都可以作为启动智能体会话的入口。完成第一个小更改后，将从筛选议题开始工作。

> [!NOTE]
> **Issues** 和 **Pull requests** 中的列表会自动筛选，仅显示已添加到 Copilot app 的存储库中的事项。若要查看其他存储库中的工作项，请将那些存储库也添加到应用。

## 尝试快速聊天

熟悉应用的好方法之一，就是向它询问有关**应用本身**的问题；**快速聊天**正适合此用途。快速聊天可以提问或头脑风暴，而不会创建分支或工作树，适合快速、一次性的问题，无需创建会话。

1. 在侧边栏中选择 **Chats** 旁边的 **+**，开始新聊天。如果 **Chats** 尚未显示，请选择 **Sessions** 旁边的 **+** 开始第一次聊天；之后就会显示 **Chats**。
2. 询问应用自身如何管理会话：

   ```plaintext
   How does the GitHub Copilot app use worktrees?
   ```

3. 在对话视图中阅读回复。你会了解到，每个会话都在独立的 Git 工作树中运行，因此可以并行运行多个智能体而不会相互覆盖。可以随时继续对话或开始新聊天。

## 总结与后续步骤

恭喜！你已安装 GitHub Copilot app、连接项目并熟悉工作区。你了解了如何：

- 安装应用并登录 GitHub。
- 从 GitHub 存储库添加项目。
- 熟悉工作区并在 **Issues** 中查找预置的待办事项。
- 使用快速聊天提出快速、一次性的问题。

接下来，[启动第一个智能体会话][next-lesson]，让它在游戏卡片上显示星级评分。

## 资源

- [关于 GitHub Copilot app][about-copilot-app]
- [开始使用 GitHub Copilot app][getting-started]
- [在 GitHub Copilot app 中使用智能体会话][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
