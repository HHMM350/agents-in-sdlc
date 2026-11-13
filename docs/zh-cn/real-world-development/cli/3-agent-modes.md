---
title: "第 3 课 - 智能体模式：Plan 和 Autopilot"
description: "先用 Plan 确认方案，再用 Autopilot 根据议题构建筛选功能，最后通过 Interactive 模式审查结果。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

刚才为项目添加了一个小功能，但更大的更改需要更完善的流程。GitHub Copilot CLI 可以融入组织现有的工作流，帮助团队以正确的方式构建正确的内容。本课将开启一系列课程，带你体验典型的智能体驱动开发流程：从议题着手构建功能，确保代码有效、行为符合预期，最终成功合并到项目中。

> [!NOTE]
> 后续功能开发将继续使用同一对话和分支。通常，不同文件类型的工作会使用不同分支或 PR；这里为了聚焦核心概念，会采用简化流程。

本课将：

- 从 GitHub 议题启动新的 Copilot 对话。
- 在 Plan 模式中明确需求。
- 使用 Autopilot 模式实现新功能。
- 审查代码。
- 通过 Codespaces 端口转发在浏览器中手动验证功能。

继续开发此功能时，还会更新存储库指令、自定义现有的 `quality-checks` 技能、添加 MCP 验证、创建 QA 智能体，并创建功能 PR。

## 场景

Tailspin Toys 的游戏目录不断扩充，访客需要按类别和发行商筛选游戏。待办事项中的议题描述了该功能，但类别组合等细节需要在编码前达成共识。你将先用 Plan 模式确定这些决策，再授权 Autopilot 在明确范围内实现功能。

## 背景

在开发流程中引入 AI 编码智能体，并不会改变软件开发的基本原则，反而使这些原则更加重要！大多数开发人员都会遵循类似的流程：

1. 从描述需求的已创建议题开始。
2. 制定要构建内容的计划。
3. 编写并审查代码。
4. 运行测试以验证代码。
5. 手动验证新功能。
6. 创建拉取请求（PR）。
7. 代码通过审查且持续集成流程成功后，合并代码。

> [!NOTE]
> 具体流程因团队和组织而异，但大多数流程都与上述步骤类似。

遵循这种标准流程，可以确保 AI 生成的代码满足需求，并像手写代码一样经过审查。

## 对话模式

**对话模式**控制智能体的自主程度。按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 可在模式之间切换：

- **Interactive**：你与智能体协作。智能体提出更改建议，并等待你的输入后再继续。
- **Plan**：智能体先创建计划，在此模式下不能编辑项目文件。
- **Autopilot**：智能体自主工作，包括编写代码、运行测试并不断迭代，直至任务完成。

先从 Plan 模式开始，审查计划，然后使用 Autopilot 实现计划。

## 从议题开始

开始筛选功能前，返回 Codespace，确认存储库和终端已准备就绪。

1. 返回 Codespace。如果它已停止，请先重新启动。
2. 确认星级评分 PR 已合并。
3. 如果终端尚未打开，按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux）。
4. 更新 `main`，然后为筛选功能创建分支：

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. 启动 Copilot CLI：

   ```bash
   copilot --yolo
   ```

6. 连按两次 <kbd>Tab</kbd>，打开 **Issues** 选项卡。
7. 按 <kbd>A</kbd> 显示所有议题。
8. 使用方向键选中标题为 **Allow users to filter games by category and publisher** 的议题。
9. 按 <kbd>C</kbd> 将议题添加到提示词中，并返回 **Session** 选项卡。

注意提示词现在以 `#7`（或类似编号）开头。使用 `#` 可将 GitHub 上的议题或拉取请求（PR）加入上下文。

## 规划筛选功能

规划可以先明确功能或任务的实现方式，再交给 Copilot 执行。对于复杂任务，花些时间规划总是值得的。现在切换到 Plan 模式，请 Copilot 制定计划。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 切换到 Plan 模式。确认提示词下方的模式指示器显示 **Plan**。
2. 在上一步添加的议题引用后输入以下提示词：

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot 会开始制定计划：先探索项目，再确定适当的实现方法。

3. 过程中 Copilot 可能会询问筛选功能的具体行为。请根据偏好回答，没有唯一正确答案。
4. 计划完成后，按 <kbd>Control</kbd>+<kbd>E</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>E</kbd>（Windows/Linux）展开计划。
5. 上下滚动审阅计划。
6. 如果计划中的任何部分不符合你的决定，请要求 Copilot 修改。

## 批准 Autopilot

计划已写好并审查完毕，现在开始实现。使用 Autopilot 让 Copilot 执行计划。

Autopilot 会让 Copilot 持续迭代，直到它认为问题已解决。

1. 选择 **Accept plan and build on autopilot (recommended)**，或你所安装版本中名称相似的选项。
2. 确认提示词下方的模式指示器显示 **Autopilot**。
3. 观察 Copilot 按计划迭代、生成代码并运行测试。

> [!NOTE]
> 批准后可能会立即开始实现，因此请先审查计划。如果 Copilot 报告缺少依赖项或端口冲突，请先解决设置问题，再将检查视为已完成。

## 审查并验证实现

生成的代码需要像其他代码一样，在合并前经过审查。现在检查代码并运行网站，确认一切正常。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 进入 Interactive 模式。确认模式指示器不再显示 **Plan** 或 **Autopilot**。
2. 输入 `/diff`，检查筛选功能及其测试。
3. 对照议题和规划时做出的决定审查结果。
4. 审查代码后，按 <kbd>Esc</kbd> 退出差异视图。
5. 查看项目检查结果，并请 Copilot 解决任何失败项。

## 试用新功能

代码看起来不错，但实际运行情况如何？像之前一样启动应用，通过 Codespaces 转发的端口打开网站。

1. 请 Copilot 启动应用：

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. 当 Codespaces 报告端口 `4321` 可用时，选择 **Open in Browser**。
3. 尝试按类别、发行商筛选，以及计划中确定的组合。
4. 确认重置和无结果时的行为符合议题和你的决定。
5. 返回 Codespace，请 Copilot 停止它启动的开发服务器。

## 总结与后续步骤

你使用不同的对话模式构建并审查了功能。本课中，你：

- 从 GitHub 议题启动了新的 Copilot 对话。
- 在 Plan 模式中明确了需求。
- 使用 Autopilot 模式实现了新功能。
- 审查了代码。
- 通过 Codespaces 端口转发在浏览器中手动验证了功能。

接下来，通过[自定义指令][next-lesson]进一步了解如何确保代码遵循已记录的实践。

## 资源

- [GitHub Copilot CLI 中的 Autopilot][autopilot]
- [Copilot CLI 命令参考][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
