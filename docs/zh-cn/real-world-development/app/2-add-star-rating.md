---
title: "第 2 课 - 添加星级评分：快速改进"
description: "在 GitHub Copilot app 中启动第一个智能体会话，对游戏卡片进行小幅修改，并将更改作为第一个拉取请求合并。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

熟悉工作区并尝试快速聊天后，现在开始**智能体会话**，为项目进行第一次更改。先从小处着手：游戏数据中已经包含星级评分，但主页上的游戏卡片还没有显示它。让智能体显示评分、审查更改，并将其作为第一个拉取请求合并。

本课将：

- 启动智能体会话，并了解会话的组成。
- 请智能体对项目进行小幅、专注的修改。
- 在工作区差异视图中审查更改。
- 在本地运行应用，并在浏览器中确认更改。
- 创建并合并第一个拉取请求。

## 场景

Tailspin Toys 中的每款游戏都有星级评分，而且游戏详情页已经显示该评分。但主页上的游戏卡片只显示标题、类别、发行商和描述。作为热身，请智能体在每张卡片上显示已有评分。这是一个小而独立的更改，很适合用来开始第一次会话。

## 会话的组成

**会话**是与智能体进行的对话，它在独立工作区中运行。每个会话都有专用的 **Git 工作树和分支**，因此可以同时运行多个会话，例如一个添加功能，另一个修复 bug，且更改不会相互覆盖。会话按存储库分组显示在侧边栏中；选择任意会话即可切换到该会话。

会话包含三部分：与智能体的**对话**、智能体探索和编辑文件时执行的**工具操作**，以及显示差异的**已更改文件**列表。

## 开始会话并请求更改

现在开始新会话，探索项目并实现功能。在[应用设置][prior-lesson]期间，已经通过 GitHub 存储库添加了项目。接下来为该存储库创建新会话并请求更改。

1. 返回或打开 GitHub Copilot app。
2. 选择侧边栏顶部的 **+**，开始会话。
3. 选择 `tailspin-toys` 存储库。
4. 在提示框下方选择**新工作树**和 **Interactive** 模式。使用以下提示词请求更改：

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

5. 按 <kbd>Enter</kbd> 向 Copilot 发送提示词。

Copilot app 会先创建新的工作树，也就是项目的隔离副本。然后探索项目，找到需要修改的文件并编写代码。现在已使用 Copilot app 添加了新功能！

## 审查差异

合并前应审查所有 AI 生成的更改，即使更改很小也不例外。现在直接在 Copilot app 中检查。

1. 在应用右上角选择 **Toggle review panel**。在打开的面板中选择 **Changes**，查看已更改的文件和差异。

   ![GitHub Copilot app 顶部工具栏截图，箭头指向 Create PR 右侧的 Toggle review panel 按钮](../../../_images/app-2-review-panel.png)

2. 你应该会看到 `GameCard.astro` 中添加了代码，该文件用于显示游戏详情。代码类似于以下片段：有评分时显示评分，`starRating` 为 `null` 时则显示 `No rating yet`：

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> 与所有生成式 AI 工具一样，Copilot 具有概率性而非确定性，因此生成的具体代码可能不同，但应该大致相似。

## 检查更改

打开浏览器前，先审查智能体自动检查的结果。确认测试覆盖了数字 `starRating` 和 `null` 回退状态。缺少前置条件或跳过的检查不算通过；批准任何安装请求前请先审查。

不能只阅读代码就假定一切正常。现在请 Copilot 打开网站，以便检查更新后的 UI。可以让它启动网站，并在浏览器画布中打开。

> [!TIP]
> 画布是 Copilot app 中可交互的小组件。稍后会探索自定义画布，甚至创建自己的画布；现在先使用内置的浏览器画布。

1. 使用以下提示词，请 Copilot 启动应用并在浏览器画布中打开页面：

   ```plaintext
   Start the app and open it in the browser canvas.
   ```

2. 稍等片刻，应用将启动，并在 Copilot app 中打开浏览器窗口。
3. 确认已评分的游戏卡片显示了满分为五分的评分。
4. 完成后，使用以下提示词请 Copilot 停止本会话启动的开发服务器：

   ```plaintext
   Stop the dev server and close the browser canvas.
   ```

## 创建并合并第一个拉取请求

功能已完成！接下来创建拉取请求（PR），将新代码合并到现有代码库。

1. 在右上角选择 **Create PR**。
2. 如果系统提示，请选择 **Sign in with your browser** 并按说明完成身份验证。
3. 如果 Copilot 说明存储库策略要求先关联议题才能创建 PR，请确认应按此流程操作。
4. Copilot 将开始创建 PR。
5. 选择聊天上方的 **PR** 气泡，在审查面板中打开 PR。可在此审查拉取请求。
6. 准备就绪后，选择 **Ready to merge**。
7. 在新对话框中选择 **Merge pull request**，合并拉取请求。

## 总结与后续步骤

恭喜，你使用 GitHub Copilot app 发布了第一个更改！具体来说，你：

- 启动了智能体会话，并了解会话的组成。
- 指示智能体对游戏卡片进行小幅、专注的修改。
- 在工作区差异视图中审查更改。
- 在本地运行应用，并在浏览器中确认了星级评分。
- 创建了 PR 1、审查其检查结果并明确合并。

接下来，你将[从筛选议题开始，并使用 Plan 和 Autopilot 模式][next-lesson]构建更大的功能。

## 资源

- [在 GitHub Copilot app 中使用智能体会话][agent-sessions]
- [关于 GitHub Copilot app][about-copilot-app]
- [使用 GitHub Copilot app 管理议题和拉取请求][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#安装并配置-github-copilot-app
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
