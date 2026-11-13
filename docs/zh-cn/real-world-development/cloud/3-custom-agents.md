---
title: "练习 3 - 自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

GitHub Copilot 中的[自定义智能体][custom-agents-concept]是针对开发工作流中特定任务或领域定制的 AI 助手。你可以通过存储库中的 `.github/agents` 文件夹下的 Markdown 文件定义智能体，为 Copilot 提供专注的指令、最佳实践、编码模式和领域知识，帮助它更有效地完成特定类型的工作。团队可以将专业知识编写成可复用的智能体，例如执行 [WCAG][wcag] 规范的无障碍智能体、遵循安全编码实践的安全智能体，或维护一致测试模式的测试智能体。

自定义智能体由项目 `.github/agents` 文件夹或全局 `~/.copilot/agents` 目录中的 Markdown 文件定义。每个文件都包含 YAML frontmatter，至少指定 `name` 和 `description`，后续 Markdown 提示词则定义智能体的行为、专业知识和指令。

### 自定义智能体与智能体技能的区别

自定义智能体与[智能体技能][agent-skills-concept]在概念上有所重叠。两者主要通过 Markdown 文件定义，用于指导 AI 执行操作。最简单的区分方式是：**自定义智能体**是工作者，**技能**是工具。

自定义智能体拥有自己的上下文窗口，并负责协调技能（甚至其他智能体）来完成任务。本实验中的无障碍自定义智能体会根据无障碍指引审查并更新网站；在执行过程中，它可以调用拉取请求工作流技能或用于运行和管理测试的技能。

> [!NOTE]
> 编写自定义智能体没有唯一正确的方法。与 AI 的其他用法一样，需要不断测试和迭代，找到适合环境和场景的方案。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

通过自定义智能体，你将了解：

- 如何定义自定义智能体。
- 如何向自定义智能体分配任务。

## 场景

Tailspin Toys 致力于让所有用户都能访问其众筹平台，不受视力能力或偏好的影响。近期的用户反馈指出，部分用户认为当前深色主题难以阅读，因为文本与背景颜色的对比度不足。为解决这个无障碍问题，设计团队要求实现可由用户启用或关闭的高对比度模式。

无障碍至关重要，因此希望尽快实现此功能。接下来将使用自定义智能体生成相关功能。

## 审查无障碍自定义智能体

已经为你创建了一个无障碍自定义智能体。先审查其内容，了解它将如何引导 Copilot。

返回 Codespace，然后查看无障碍自定义智能体文件：

1. 打开 `.github/agents/accessibility.md`。
2. 留意包含 `name` 和 `description` 字段的 YAML frontmatter。

> [!CAUTION]
> `name` 和 `description` 是自定义智能体必需的 frontmatter 字段。

3. 接着浏览后续各节，查看其中说明的内容：
   - 为无障碍网站生成代码时的核心职责。
   - 无障碍最佳实践。
   - HTML、CSS 和 JavaScript 代码示例。
   - 常见问题和错误清单。

## 创建并分配议题

任务控制中心是管理环境中所有智能体的中心位置。你可以在此处向 Copilot cloud agent 分配任务、监控任务并引导工作。现在向 Copilot 分配一个实现高对比度模式的任务。

1. 打开存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 创建空白议题。
5. 将 **Title** 设置为 `Add high contrast mode to website`。
6. 将 **Description** 设置为：

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。
9. 从自定义智能体列表中选择 **Accessibility agent**。

   ![cloud agent 分配界面截图，突出显示自定义智能体和 Accessibility agent](../../../_images/ex5-select-custom-agent.png)

10. 选择 **Assign**。
11. Copilot 将在后台开始处理任务！

## 总结与后续步骤

本课介绍了 GitHub Copilot 中的[自定义智能体][custom-agents]，也就是针对特定任务和领域定制的 AI 助手。借助自定义智能体，可以将团队专业知识和标准编写成可复用角色，更有效地指导 Copilot 完成特定类型的工作。

本课中，你了解了：

- 如何定义自定义智能体。
- 如何向自定义智能体分配任务。

Copilot 正在实现高对比度模式。接下来，从任务控制中心[监控并引导智能体会话][next-lesson]。

## 资源

- [关于自定义智能体][custom-agents]
- [为组织使用自定义智能体做好准备][org-custom-agents]
- [为企业使用自定义智能体做好准备][enterprise-custom-agents]

---

| [← 上一课：GitHub Copilot cloud agent][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
