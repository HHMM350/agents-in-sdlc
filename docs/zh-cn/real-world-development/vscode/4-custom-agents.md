---
title: "练习 4 - 自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

GitHub Copilot 中的[自定义智能体][custom-agents-concept]是针对开发工作流中特定任务或领域定制的 AI 助手。通过在存储库的 `.github/agents` 文件夹中创建 Markdown 文件，可以为 Copilot 提供专注的指令、最佳实践、编码模式和领域知识，帮助它更有效地完成特定类型的工作。团队可以将专业知识编写成可复用的智能体，例如执行 [WCAG][wcag] 规范的无障碍智能体、遵循安全编码实践的安全智能体，或维护一致测试模式的测试智能体。

自定义智能体由项目 `.github/agents` 文件夹或全局 `~/.copilot/agents` 目录中的 Markdown 文件定义。每个文件都包含 YAML frontmatter，至少指定 `name` 和 `description`，后续 Markdown 提示词则定义智能体的行为、专业知识和指令。

### 自定义智能体与智能体技能的区别

自定义智能体与[智能体技能][agent-skills-concept]在概念上有所重叠。两者主要通过 Markdown 文件定义，用于指导 AI 执行操作。最简单的区分方式是：**自定义智能体**是工作者，**技能**是工具。

自定义智能体拥有自己的上下文窗口，并负责协调技能（甚至其他智能体）来完成任务。本实验中的无障碍自定义智能体会根据无障碍指引审查并更新网站；在执行过程中，它可以调用拉取请求工作流技能或用于运行和管理测试的技能。

> [!NOTE]
> 编写自定义智能体没有唯一正确的方法。与 AI 的其他用法一样，需要不断测试和迭代，找到适合环境和场景的方案。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## 场景

Tailspin Toys 致力于让所有用户都能访问其众筹平台，不受视力能力或偏好的影响。近期的用户反馈指出，部分用户认为当前深色主题难以阅读，因为文本与背景颜色的对比度不足。为解决这个无障碍问题，设计团队要求实现可由用户启用或关闭的高对比度模式。

无障碍至关重要，因此希望尽快实现此功能。接下来将使用自定义智能体生成相关功能。

本练习将：

- 审查已有的无障碍自定义智能体。
- 在 Copilot Chat 中使用无障碍智能体实现高对比度模式。

## 审查无障碍自定义智能体

已经为你创建了一个无障碍自定义智能体。先审查其内容，了解它将如何引导 Copilot。

返回 codespace，打开终端，并从 `main` 创建新分支，用于无障碍功能开发（筛选功能 PR 将在练习 3 中单独保留）：

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. 打开 `.github/agents/accessibility.md`。
2. 留意包含 `name` 和 `description` 字段的 YAML frontmatter。

> [!CAUTION]
> `name` 和 `description` 是自定义智能体必需的 frontmatter 字段。

3. 接着浏览后续各节，查看其中说明的内容：
   - 为无障碍网站生成代码时的核心职责。
   - 无障碍最佳实践。
   - HTML、CSS 和 JavaScript 代码示例。
   - 常见问题和错误清单。

## 在 Copilot Chat 中使用自定义智能体

VS Code 会在 Copilot Chat 视图底部的智能体下拉列表中显示 `.github/agents` 中定义的所有自定义智能体。选择自定义智能体后，聊天会话将遵循该智能体的指令并使用它的工具。

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。不同练习所用模式和模型可能不同；每个步骤会在适用时说明。

1. 如果智能体下拉列表中尚未选中 **Agent**，请选择它。

   ![Chat 视图中智能体选择器的截图](../../../_images/shared-chat-mode-selector.png)

2. 选择 Chat 视图底部的智能体下拉列表（其中显示当前智能体，默认是 **default**）。
3. 从可用智能体列表中选择 **Accessibility agent**。
4. 向无障碍智能体发送以下提示词：

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

5. Copilot Chat 会开始工作，探索代码库、提出更改建议并编辑项目文件。每项编辑都会以内嵌形式显示在聊天中，并包含文件路径和可审查的差异。
6. 随着编辑逐步完成，**Files changed** 指示器会更新，显示智能体修改的工作集。

> [!NOTE]
> 此过程可能需要几分钟。Copilot 会修改存储库中的真实文件，包括 Astro 组件、CSS 和相关测试。

下一练习将审查并引导这项正在进行的工作。

## 总结与后续步骤

本课介绍了 GitHub Copilot 中的[自定义智能体][custom-agents]，也就是针对特定任务和领域定制的 AI 助手。借助自定义智能体，可以将团队专业知识和标准编写成可复用角色，更有效地指导 Copilot 完成特定类型的工作。

本课中，你了解了：

- 如何定义自定义智能体。
- 如何在 Copilot Chat 代理模式中使用自定义智能体。

接下来，[监控并引导智能体工作][next-lesson]，在更改产生时进行审查，并在同一会话中添加浅色模式切换。

## 资源

- [关于自定义智能体][custom-agents]
- [在 IDE 中创建自定义智能体][creating-custom-agents-ide]
- [VS Code 中的自定义智能体][custom-agents-vscode]
- [自定义智能体配置][custom-agents-config]
- [awesome-copilot 中的自定义智能体][awesome-copilot-agents]

---

| [← 上一课：使用 Playwright MCP 服务器测试功能][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
