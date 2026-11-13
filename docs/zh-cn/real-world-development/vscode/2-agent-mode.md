---
title: "练习 2 - 使用 Copilot 代理模式添加新功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

即使是最简单的应用更新，通常也需要修改多个文件并执行一些操作，例如运行测试。开发人员通常需要查找所有相关文件、进行更改、运行测试、调试、找出遗漏的文件并再次修改……流程会不断重复。

Copilot 代理模式正是为此而设计的。

Copilot 代理模式可以在 IDE 中更自主地工作。它的行为类似开发人员：先探索现有项目结构，再执行必要的更新、运行测试等任务，并自动修复发现的问题。接下来了解如何使用代理模式为网站添加新功能。

> [!NOTE]
> 代理模式和 cloud agent 名称相似，但适用于两种不同的体验。代理模式在 IDE 中执行任务，可快速获得反馈并与智能体互动。cloud agent 则像团队成员一样异步工作，通过议题和拉取请求与你协作。

本练习将了解：

- Copilot 代理模式如何探索项目、识别相关文件并协同修改多个文件。
- GitHub Copilot 代理模式如何跨 UI 和数据层实现新功能。
- 合并到代码库之前，如何审查 Copilot 代理模式生成的更改和测试。

## 场景

游戏列表不断增长，你希望让用户按类别和发行商筛选。上一练习已添加发行商辅助函数；现在将使用 Copilot 代理模式完成剩余的数据层、UI 和测试工作。

## 运行 Tailspin Toys 网站

进行更改前，先浏览 Tailspin Toys 网站，了解现有功能。

网站是一个带有开发者主题的桌游众筹平台，可列出游戏并显示详情。它是一个单独的 Astro 应用，构建时会将页面渲染为静态 HTML。页面在 frontmatter 中通过 Drizzle ORM 直接查询本地 SQLite 数据库；没有独立后端 API 或客户端 UI 框架。可复用的数据访问辅助函数位于 `src/lib/`，交互功能由使用标准 DOM API 的小型局部 Astro `<script>` 实现。

### 启动网站

项目提供了 `npm run dev` 任务，用于启动单个 Astro 开发服务器。请按以下步骤在 GitHub Codespace 中运行：

1. 返回 codespace。上一练习结束后，你应该已切回 `main`。
2. 按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux），在 Codespace 中打开新终端。
3. 为筛选功能创建并切换到新分支：

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 运行以下命令启动网站：

   ```bash
   npm run dev
   ```

   Astro 开发服务器就绪后，会显示类似以下内容的横幅：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> 如果弹出对话框，询问是否要打开 `http://localhost:4321` 的浏览器窗口，请选择 **x** 将其关闭。

5. 在终端中按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），同时选择 Astro 服务器地址 `http://localhost:4321`，打开网站。

> [!NOTE]
> 在 codespace 中选择终端里的 localhost URL 链接时，会自动重定向到 `https://<your-codespace-name>-4321.app.github.dev/`。这是指向 codespace 的私有隧道，网站服务器正在其中运行。

### 浏览网站

网站运行后，可以浏览现有功能。主要功能包括：

- **主页**：显示桌游列表，包括标题、图片和描述。
- **游戏详情页**：选择游戏后会打开详情页，其中包含标题、描述、发行商和类别等信息。

## 使用 Copilot 浏览待办事项

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。不同练习所用模式和模型可能不同；每个步骤会在适用时说明。

网站初始版本可以正常运行，但还需要添加更多功能。先查看待办事项。通过模板设置项目时，系统已自动创建一组议题；请 GitHub Copilot 显示这些事项。

1. 在 Chat 视图的智能体下拉列表中选择 **Agent**。Agent 智能体会自主规划并跨文件实现更改、运行终端命令并调用工具。

   ![Chat 视图中智能体选择器的截图](../../../_images/shared-chat-mode-selector.png)

2. 从可用模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 本研讨会作者并未偏好某一模型。编写研讨会时使用的是 Claude Sonnet 4.5，因此文档中采用该模型，希望由此获得相对一致的代码建议。由于 LLM 具有概率性，你看到的建议可能与研讨会示例不同，这是正常且预期的情况。

> [!NOTE]
> 由于 LLM 具有概率性，Copilot 可能会使用不同的 MCP 命令，但仍应能完成任务。

3. 向 Copilot 发送以下提示词，询问待办事项：

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. 选择 **Continue** 以运行列出所有议题的命令。
5. 审查生成的议题列表。

留意 Copilot 还根据它认为对用户最有用的事项为列表排了优先级。

## 审查指令文件

让智能体生成代码前，先查看将用于提供上下文的指令文件。项目中的[用户界面 (UI) 指令文件](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)介绍了如何为网站添加功能。

1. 在 codespace 中打开 `.github/instructions/ui.instructions.md`。
2. 留意其中的整体功能实现指引，包括：
   - 架构概述。
   - 组件设计、可测试性和无障碍原则。
   - 指向多种文件类型对应指令的链接，包括：
     - Astro
     - Tailwind CSS
     - Drizzle

> [!TIP]
> 指令文件可以引用其他指令文件和项目中的文件。路径相对于指令文件所在位置，因此可以复用指令、将复杂内容拆分为较小的模块，并提供示例和模板。

## 实现筛选功能

完成筛选功能至少需要对应用进行三项更改：

- 在数据层 (`src/lib/`) 添加或完善剩余的筛选逻辑。
- 添加或更新筛选行为的测试。
- 更新游戏列表页面，加入筛选 UI。

此外，合并前还需要运行并通过测试。Copilot 代理模式可以为你完成这些任务！现在开始添加功能。

1. 可以继续当前 Copilot 对话，也可以选择 **New Chat** 开始新对话。
2. 选择 **Add Context**、**Instructions**，然后选择 `ui` 指令文件。

   ![选择 UI 指令文件的示例](../../../_images/ex3-select-instructions-file.png)

3. 确认 Chat 视图的智能体下拉列表中仍选中 **Agent**。

   ![Chat 视图中智能体选择器的截图](../../../_images/shared-chat-mode-selector.png)

4. 确认仍选择 **Claude Sonnet 4.5** 模型。
5. 使用以下提示词，让 Copilot 根据待办事项中的相关议题实现功能：

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. 观察 Copilot 如何探索项目并查找相关文件。它应该找到数据层辅助函数、UI 和测试，然后开始修改文件并运行测试。

   ![Copilot 正在探索项目文件的截图](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot 会执行多项任务，例如探索项目、修改文件和运行测试。具体耗时取决于任务复杂度和代码库规模，可能需要几分钟。在此过程中，代码编辑器可能会出现 **Keep** 和 **Undo** 按钮。Copilot 完成后，每项更改都会有 **Keep** 或 **Undo** 选项，因此无需在工作过程中提前选择。

7. Copilot 提示时，选择 **Continue** 运行测试。

   ![Copilot Chat 面板中的对话框截图，询问用户是否允许运行测试](../../../_images/ex3-agent-mode-run-tests.png)

8. 过程中可能会有暂停，甚至出现测试失败。这没有关系！Copilot 会在代码生成和测试之间不断迭代，直至任务完成且未发现错误。

   ![已完成的 Copilot 代理模式 Chat 会话截图](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 检查生成的代码，查看是否存在潜在问题。

> [!CAUTION]
> 请始终审查 Copilot 或其他 AI 工具生成的代码。

10. 返回正在运行网站的浏览器，体验新功能。
11. 确认功能正常并审查代码后，在 Copilot Chat 窗口中选择 **Keep**。

## 总结与后续步骤

恭喜！本练习介绍了如何使用 GitHub Copilot 代理模式为 Tailspin Toys 网站添加新功能。你了解了：

- GitHub Copilot 代理模式如何跨 UI 和数据层实现新功能。
- Copilot 代理模式如何探索项目、识别相关文件并协同修改多个文件。
- 合并到代码库之前，如何审查 Copilot 代理模式生成的更改和测试。

接下来，[使用 Playwright MCP 服务器测试功能][next-lesson]，并为其创建拉取请求。

### 附加探索练习 — 实现分页

随着游戏列表不断增长，网站将需要分页功能。运用本练习所学知识，请 Copilot 更新网站并实现分页。编写提示词时可以考虑：

- 遵循现有最佳实践，包括使用已有指令文件。
- 考虑分页方式：允许用户选择每页大小，还是使用固定值。
- 为 Copilot 提供所需指导，确保实现方式符合预期。
- 可能需要通过迭代让 GitHub Copilot 修改实现并补充上下文。这是与 Copilot 协作的正常流程！

## 资源

- [Copilot 的 ask、edit 和 agent 模式：功能及适用场景][choose-mode]
- [VS Code 中的代理模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
