---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

在前几项练习中，你让 Copilot cloud agent 执行了三个改善用户体验和添加功能的任务。cloud agent 虽然可以异步自主工作，但监控这些任务仍然很重要。

有多种工具可用于管理分配给 cloud agent 的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个任务控制中心，可以查看所有创建了未关闭拉取请求（PR）的智能体任务，了解已执行的操作，甚至可以引导正在进行的会话。

本课将：

- 浏览智能体页面，监控 cloud agent 任务。
- 引导正在进行的会话，请求添加其他功能。

## 场景

将实现高对比度模式的任务交给智能体后，团队意识到也可以顺便添加浅色模式。既然正在更新网站样式并添加切换功能，一并添加浅色模式就很合理。现在需要引导智能体，确保它同时实现浅色模式和高对比度模式。

## 审查 Copilot cloud agent 任务

查看当前分配给 Copilot cloud agent 的所有任务状态。

1. 打开 [Copilot agents 页面](https://github.com/copilot/agents)。
2. 查看主面板和左侧面板中的任务列表。应能看到分配给 Copilot 的任务，包括：
   - 更新代码文档。
   - 生成用于修改游戏的 API。
   - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，查看 Copilot 已执行的操作，例如：
   - 从存储库检出代码。
   - 为 Copilot 创建工作环境。
   - 设置 MCP 服务器。
   - 执行完成所分配任务所需的各项操作。

> [!NOTE]
> 具体显示的步骤因 Copilot 的工作状态和采用的方法而异。

4. 同时留意右侧显示的 PR 面板。你可以在此查看 PR 和更改的文件，以便进一步监控。

## 引导 cloud agent

现在已经查看了正在执行的任务，请求 Copilot 在实现高对比度模式时也添加浅色模式。

1. 选择与添加高对比度模式有关的会话。确切标题会因 Copilot 使用的名称和当前工作状态而异。

   ![任务控制中心中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，直到 Copilot 完成设置并开始工作。出现类似下方的消息时，就表示它已开始处理任务。
3. 在 **Steer active session while Copilot is working** 对话框中，添加以下提示词：

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![Copilot agents 页面中的 cloud agent 任务截图，突出显示 Steer active session while Copilot is working 对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示词。
5. 留意 Copilot 如何确认收到提示词，并将它加入工作流程。

## 让 Copilot 继续工作

和之前一样，Copilot 会继续处理更新后的任务！它会在完成你发送消息时正在执行的步骤后，将新请求加入工作流程。

与之前一样，这需要几分钟。此时可以暂停一下，回顾目前学到和体验的内容。

## 总结与后续步骤

本课介绍了 Copilot agents 页面，这是监控和引导 GitHub Copilot cloud agent 任务的中心位置。借助此任务控制中心，可以跟踪所有正在进行和已完成的任务、审查已执行的工作，甚至可以重定向正在进行的任务以调整范围或补充指导。

本课中，你：

- 浏览了任务控制中心和智能体页面，监控 cloud agent 任务。
- 重定向了正在进行的会话，请求添加其他功能。

Copilot 正在完成无障碍功能，接下来将[迭代改进它创建的拉取请求][next-lesson]。

## 资源

- [Copilot agents 页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代改进 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
