---
title: "第 2 课 - 添加星级评分：快速改进"
description: "使用 Copilot CLI 修改游戏卡片，在浏览器中检查结果，并将更改作为第一个拉取请求合并。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

安装 Copilot CLI 并尝试过对话后，现在来为项目做第一个更改。先从小处着手：游戏数据中已经包含星级评分，但主页上的游戏卡片还没有显示它。让智能体显示评分、审查更改，并将其作为第一个拉取请求合并。

本课将：

- 在功能分支上启动专注于单一任务的 Copilot 对话。
- 请智能体对项目进行小幅修改。
- 使用 `/diff` 审查更改。
- 运行应用，并在浏览器中确认更改。
- 创建并合并第一个拉取请求。

## 场景

Tailspin Toys 中的每款游戏都有星级评分，而且游戏详情页已经显示该评分。但主页上的游戏卡片只显示标题、类别、发行商和描述。作为热身，请智能体在每张卡片上显示已有评分。这是一个小而独立的更改，很适合用来开始第一次会话。

## 对话的组成

**对话**是使用 Copilot CLI 完成任务的工作区。与 Copilot app 不同，普通 CLI 对话会使用终端当前检出的存储库和 Git 分支，而不是创建专用工作树。保存的对话可供日后继续，但文件和分支仍是磁盘上的普通 Git 状态。

对话包含三部分：你的提示词和智能体的回复；智能体探索和编辑文件时执行的工具操作；以及可通过 `/diff` 检查的更改。

## 开始对话并请求更改

创建新对话，开始实现功能。

1. 返回 Codespace。
2. 如果终端尚未打开，按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux）。
3. 如果 Copilot 尚未运行，执行以下命令：

   ```bash
   copilot --yolo
   ```

4. 使用斜杠命令 `/new` 并按 <kbd>Enter</kbd>，确保已启动新会话。
5. 使用以下提示词请求更改：

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot 会探索项目，找到显示游戏详情的文件，并创建所需代码。现在已使用 Copilot CLI 添加了新功能！

## 审查差异

合并前应审查所有 AI 生成的更改，即使更改很小也不例外。现在直接在 Copilot CLI 中检查更改。

1. 输入 `/diff` 并检查所有已更改的文件。
2. 确认游戏卡片在评分存在时显示数字评分，在 `starRating` 为 `null` 时显示 `No rating yet`。
3. 确认测试覆盖了这两种状态。
4. 检查 Copilot 运行的检查结果，并要求它修复任何失败项。
5. 审查完毕后，按 <kbd>Esc</kbd> 退出差异界面。

> [!NOTE]
> 与所有生成式 AI 工具一样，Copilot 具有概率性而非确定性，因此生成的具体代码可能不同。应审查实际行为，而不是要求实现与某个示例完全相同。

## 检查更改

当然，不能只阅读代码就假定一切正常。让 Copilot 启动网站，然后通过 Codespaces 端口转发在浏览器中检查更新后的界面。

1. 请 Copilot 启动应用：

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. 当 Codespaces 报告端口 `4321` 可用时，选择 **Open in Browser**。
3. 确认游戏卡片显示了满分为五分的星级评分。
4. 返回 Copilot，并要求它停止启动的服务器：

   ```plaintext
   Stop the development server you started.
   ```

## 创建并合并第一个拉取请求

功能已完成！接下来创建拉取请求（PR），将新代码合并到项目中。

1. 请默认智能体提交更改：

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. 输入 `/pr create`。Copilot CLI 会在创建 PR 时推送现有提交，并显示 PR URL。
3. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），同时选择 Copilot CLI 显示的 URL，以打开 PR。
4. 审查更改的文件和检查结果。
5. 准备就绪后，选择 **Merge pull request**，然后确认合并。
6. 返回 Codespace，使用 `/exit` 退出 Copilot CLI。
7. 更新本地 `main`：

   ```bash
   git checkout main
   git pull
   ```

## 总结与后续步骤

恭喜，你使用 GitHub Copilot CLI 发布了第一个更改！具体来说，你：

- 在功能分支上启动了专注于单一任务的 Copilot 对话。
- 指示智能体修改游戏卡片。
- 使用 `/diff` 审查更改。
- 运行应用，并在浏览器中确认了星级评分。
- 创建并合并了第一个拉取请求。

接下来，你将[从筛选议题开始，并使用 Plan 和 Autopilot 模式][next-lesson]构建更大的功能。

## 资源

- [关于 GitHub Copilot CLI][about-copilot-cli]
- [Copilot CLI 命令参考][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
