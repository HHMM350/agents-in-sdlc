---
title: "练习 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义指令][previous-lesson] |
|:--|

几乎所有组织都会遇到技术债务问题，例如尚未解决的安全问题、需要更新的旧代码，或因缺少时间而长期搁置的功能请求。GitHub Copilot cloud agent 可以自主执行更新代码和添加功能等任务。完成后，它会创建一个草稿 PR，供开发人员审查。这样可以将繁琐任务交给智能体，加快开发流程，让开发人员专注于更重要的工作。

你将通过 Copilot cloud agent 了解以下内容：

- 如何自定义代码生成环境。
- 如何确保操作安全。
- 明确界定议题范围的重要性。
- 如何向 Copilot 分配议题。

## 场景

Tailspin Toys 有一些技术债务需要处理。最初受雇开发网站的承包商没有留下完善的文档，事实上，你会发现项目完全缺少文档。首先，他们希望为应用程序中所有导出的函数添加 TSDoc 文档注释。

此外，设计团队准备改善游戏发现体验。他们希望每款游戏的详情页显示相关游戏，也就是其他同类别的游戏，方便用户继续浏览。目前不要求实现经过润色的版本，只需要能用于用户体验验收测试的功能。虽然这项工作目前受阻，但还有优先级更高的议题需要处理。

这两项任务都可能很快被降级为低优先级，非常适合交给 Copilot cloud agent。它可以异步处理任务，让开发人员先处理其他工作，之后再回来审查 Copilot 的成果并确认符合预期。

## 了解 GitHub Copilot cloud agent

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) 可以像人类开发人员一样在后台执行任务。与委派给人类开发人员类似，有多种方式启动工作，其中包括[将 GitHub 议题分配给 Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)。分配任务后，Copilot 会创建草稿拉取请求来跟踪进度、设置工作环境并开始处理任务。无论任务是否完成，你都可以查看 Copilot 会话。解决方案准备好供审查时，Copilot 会在拉取请求中通知你。

## 明确指令范围的重要性

GitHub Copilot 并非魔法——使用它并不意味着可以跳过思考。即使看似简单的操作，也可能包含复杂细节，因此[请谨慎界定分配给 Copilot cloud agent 的任务范围][cloud-agent-best-practices]。应将它视为 AI 结对程序员：分阶段工作、不断学习、试验和调整。引入生成式 AI 并不会改变软件开发的基本原则。

## 本存储库中的自定义指令

前面的练习介绍了自定义指令及其如何引导 Copilot。如果已经学习过自定义指令的实践课程，就会看到 `.github/copilot-instructions.md` 的作用；如果尚未学习，现在可以快速查看。将任务分配给 Copilot cloud agent 前，先只读查看存储库中已有的指令文件，稍后便能观察其影响。

在 GitHub 网页界面中打开以下文件；如果已启动 codespace，也可以在那里查看：

- `.github/copilot-instructions.md`：检查 **Code standards** 部分，特别是 TypeScript 规范和 TSDoc 文档注释要求。
- `.github/instructions/unit-tests.instructions.md`：留意 `applyTo` frontmatter，它将指令限定为 `**/*.test.ts` 文件。

下一节将 `Code lacks documentation` 议题分配给 cloud agent 时，请留意生成的 PR 是否包含 TSDoc 文档注释、TypeScript 规范和注释头。这些内容来自上述指令文件。后续练习审查 PR 时还会再次提到这些要求。

## 为 Copilot cloud agent 设置开发环境

无论由谁编写代码，通常都需要特定环境并运行一些设置脚本，确保所有依赖项和工具就绪。将任务分配给 Copilot 时也一样，因为它会以类似软件工程师的方式工作。

cloud agent 使用 [GitHub Actions][github-actions] 作为工作环境。可以通过创建[专用设置工作流][setup-workflow]来自定义环境，该工作流配置在 `.github/workflows/copilot-setup-steps.yml` 中，并会在 cloud agent 开始工作前运行。这样可以确保它获得所需的开发工具和依赖项。实验已预先配置此工作流，以便顺利完成课程并体验相应功能。它会为单体 Astro 应用安装 Node.js 和项目依赖项、下载端到端测试所需的浏览器二进制文件，并迁移和填充 SQLite 数据库：

```yaml
name: "Copilot Setup Steps"

# 可在存储库的“Actions”选项卡中测试这些设置步骤
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 只授予这些步骤所需的最低权限。Copilot 会获得自己的操作令牌。
    permissions:
      # 例如，如果需要在设置步骤中克隆存储库以安装依赖项，则需要 `contents: read` 权限。如果设置步骤不克隆存储库，Copilot 会在步骤完成后自动克隆。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # 前端/应用设置 - Node.js（整个应用现在是 Astro + Drizzle/libSQL）
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # 迁移并填充本地 SQLite 数据库，为构建和测试准备数据。
      - name: Set up the database
        run: npm run db:setup
```

这看起来与其他 GitHub 工作流文件类似，但有几点需要注意：

- 其中只有一个名为 `copilot-setup-steps` 的作业。Copilot 开始处理拉取请求前，GitHub Actions 会运行此作业。
- 留意 `workflow_dispatch` 触发器。它允许你从存储库的 **Actions** 选项卡手动运行工作流，以便测试工作流是否成功，而不用等待 Copilot 启动它。

## 添加文档

大家都知道文档很重要，但多数项目的文档要么过时，要么根本不存在。这种技术债务往往无人处理，会拖慢开发效率、增加代码库维护难度，也让新开发人员更难上手。幸运的是，Copilot 擅长创建文档，因此这是分配给 Copilot cloud agent 的理想任务。它会在后台生成所需文档，之后的练习中再回来审查结果。

1. 在新的浏览器标签页中打开 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 创建新议题。
5. 将 **Title** 设置为 `Code lacks documentation`。
6. 将 **Description** 设置为：

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。

   ![将议题分配给 Copilot](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。
10. 选择 **Pull Requests** 选项卡。
11. 打开刚创建的拉取请求（PR），标题可能类似于 `[WIP]: Code lacks documentation`。如果列表中没有新 PR，请稍等片刻并刷新浏览器窗口。
12. 几分钟后，Copilot 应该会创建待办事项清单。

> [!NOTE]
> Copilot 可能需要几分钟才能在 PR 中显示待办事项清单。Copilot 正在创建工作环境（运行前面介绍的工作流）、分析项目并确定解决问题的最佳方法。

13. 审查清单和 Copilot 即将执行的任务。
14. 向下滚动 PR 时间线，查看 Copilot 已开始处理议题的更新。
15. 选择 **View session** 按钮。

   ![Copilot 会话视图](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 可能需要刷新窗口才能看到更新后的状态指示器。

16. 浏览实时会话，了解 Copilot 如何解决问题，包括探索代码、了解当前状态、暂停思考并确定合适的计划，以及编写代码。

这可能需要几分钟。Copilot cloud agent 的一个主要目标是异步执行任务，让我们可以专注于其他工作。现在正好利用这一特点：让 Copilot cloud agent 接手另一项任务，同时我们着手为应用添加功能。

## 为游戏详情页添加相关游戏

如前所述，GitHub Copilot cloud agent 的一个主要优势是可以拆分工作：你专注于一组任务，而它处理另一组。为设计团队添加相关游戏功能可能用不了太久，但这段时间也可以用于其他工作。现在将任务分配给 Copilot cloud agent！

1. 返回 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 使用空白模板。
5. 将 **Title** 设置为 `Show related games on the game details page`。
6. 将 **Description** 设置为：

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。

   ![将议题分配给 Copilot](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

稍后，你会看到议题中的第一条评论旁出现一组 👀，表示 Copilot 已开始处理任务！

![Copilot 用眼睛表情符号表示正在处理议题](../../../_images/ex4-issue-eyes-emoji.png)

Copilot 正在认真处理第二项请求！Copilot cloud agent 的工作方式类似软件工程师，因此不需要主动监控，而是在完成后审查即可。接下来，了解如何创建和使用自定义智能体。

## 总结与后续步骤

本课介绍了 [GitHub Copilot cloud agent][copilot-agents]。可以将议题分配给 cloud agent，让 Copilot 异步处理。它可以帮助清理技术债务、创建新功能，或协助将代码迁移到其他框架。

你了解了以下内容：

- 如何自定义代码生成环境。
- 如何确保操作安全。
- 明确界定议题范围的重要性。
- 如何向 Copilot 分配议题。

cloud agent 正在后台工作，现在可以着手创建并使用自定义智能体。[Copilot cloud agent 也可以使用 MCP 服务器][cloud-agent-mcp]，并且可以使用前面模块介绍的自定义指令。

## 资源

- [关于 Copilot cloud agent][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot cloud agent 设置工作流最佳实践][cloud-agent-best-practices]

| [下一课：自定义智能体 →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
