---
title: "练习 1 - 自定义指令（Cloud agent）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：Copilot cloud agent →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务需要以特定方式完成，或者 Copilot 需要了解一些背景信息，就应确保它能够获取这些上下文。[指令文件][instruction-files]可以提供这些指导，让 Copilot 不仅了解要做什么，也了解应如何完成。

本练习将：

- 了解如何通过存储库自定义指令和按路径限定的指令文件，为 Copilot 提供项目背景、编码准则和文档规范。
- 在 `.github/copilot-instructions.md` 中添加一条适用于整个存储库的新标准。

> [!NOTE]
> 与 VS Code 和 CLI 工作环境不同，这里不会运行前后对比提示词。Copilot cloud agent 会异步处理 GitHub 议题，因此较难实时并排展示指令的影响。在本工作环境后续审查 cloud agent 创建的拉取请求时，可以看到指令文件发挥的作用。

## 指令文件

### 场景

Tailspin Toys 和许多优秀的开发团队一样，制定了一系列开发规范和要求，包括：

- 数据层始终需要单元测试。
- UI 应采用深色模式并具有现代感。
- 应使用 TSDoc 文档注释为代码添加说明。
- 每个文件开头都应添加一段注释，说明文件的用途。

通过使用指令文件，可以确保 Copilot 获取正确的信息，并按照这些规范完成任务。

### 自定义指令

自定义指令可向 Copilot 提供上下文和偏好设置，帮助它更好地理解你的编码风格和要求。你可以指定编码规范、库，以及偏好的注释形式，从而引导 Copilot 提供更相关的建议和代码片段。可以为整个存储库创建指令，也可以针对特定文件类型或任务创建指令。

指令文件有两种：

- `.github/copilot-instructions.md`：每次针对该存储库提出请求时，都会将这个单独的指令文件发送给 Copilot。文件应包含适用于大多数 Copilot Chat 或 CLI 请求的项目级信息，例如技术栈、项目概述、最佳实践和全局指导。
- `.github/instructions/*.instructions.md`：可以为特定任务或文件类型创建这些文件。例如，为 TypeScript 或 Astro 编写指引，或者为创建 UI 组件或单元测试提供指导。

> [!NOTE]
> 在 IDE 中，指令文件仅用于 Copilot Chat 生成代码，不用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot cloud agent 在生成代码时都会使用存储库级指令文件和带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> 此外，Copilot 还[支持其他规范中的指令文件][custom-instructions-support]，包括 AGENTS.md 和 CLAUDE.md 文件。

### 管理指令文件的最佳实践

完整讨论如何创建指令文件超出了本研讨会的范围。不过，示例项目展示了具有代表性的方法。总体而言：

- 让 `copilot-instructions.md` 聚焦于项目级指导，例如项目内容、项目结构和全局编码标准。
- 使用 `*.instructions.md` 为特定文件类型（如单元测试、Astro 组件和数据层）或特定任务提供指导。
- 使用自然语言，保持指导清晰，并提供代码示例说明推荐和不推荐的写法。

创建指令文件没有唯一正确的方法，使用 AI 也是如此。通过试验，逐渐找到适合项目的方法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应配备完善的指令文件。在探索本项目的文件时，可能会发现其中包含多种任务的指引，例如 [UI 更新][ui-instructions]和 [Astro][astro-instructions]。
>
> Copilot 也可以帮助生成指令文件。不同产品界面的入口有所不同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。当前工作环境的课程会在适用时介绍对应的入口。
>
> 需要模板或起点？可以浏览 [awesome-copilot][awesome-copilot]，其中收集了指令文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 浏览本项目中的自定义指令文件

花些时间阅读此存储库自带的指令文件：一个核心 `copilot-instructions.md` 文件，以及一组面向不同任务的 `*.instructions.md` 文件。可以在编辑器或 GitHub 网页界面中打开这些文件。

1. 打开 `.github/copilot-instructions.md`。
2. 浏览文件，留意项目简介，以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。在 **Code standards** 下，留意嵌套的 **GitHub Actions Workflows** 指引。这些指引适用于与 Copilot 的各种交互。
3. 打开 `.github/instructions` 文件夹并浏览其中内容。注意这里有 Astro 文件、Drizzle 数据层、测试等方面的指令。
4. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` 字段，它设置了相对于存储库根目录的 glob，用于确定指令适用于哪些文件。此处会匹配所有 TypeScript 测试文件，例如符合 `**/*.test.ts` 的文件。
5. 留意该项目针对单元测试的具体指令。
6. 最后，打开 `.github/instructions/drizzle.instructions.md` 并滚动到文件底部。留意其中指向其他指令文件（如 `unit-tests.instructions.md`）和项目现有文件的链接。此处的路径相对于指令文件，而不是存储库根目录。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分介绍了项目的编码标准，但尚未要求添加代码内文档。接下来将添加 TSDoc 文档注释和文件注释头的规则。

## 添加新的存储库标准

接下来要做的是在此处唯一一次编辑：添加一条项目级规则，要求使用 TSDoc 文档注释为代码添加说明，并在文件开头添加注释头。cloud agent 之后处理本工作环境中分配的议题时会遵循这条规则。

编辑前，先创建一个分支（cloud agent 会从议题目标分支读取指令，但仍应将自己的更改整洁地提交）：

1. 在 codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

如前所述，`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。接下来，为存储库编码标准添加文档要求，以改进代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分，通常在第 27 行附近。注意该部分介绍了项目的编码标准，但尚未要求添加代码内文档，这也是生成的辅助函数没有文档注释的原因。
3. 在现有标准下方添加以下 Markdown 内容，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 如上一课所示，可以在存储库级别（`.github/copilot-instructions.md`）创建指令文件，提供全局指导；也可以使用 `*.instructions.md` 为特定语言、文件类型或任务提供指导。刚刚添加的文档注释规则属于项目级标准，因此存储库级文件是合适的位置。

## 提交、推送并合并指令更新

cloud agent 会读取议题目标分支上的指令文件。在下一课将议题分配给 Copilot 时，它会从 `main` 创建分支，因此必须先将指令更改合并到 `main`，cloud agent 才能使用这些指令。

1. 暂存并提交更改：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 合并到 `main` 的拉取请求，并合并。这样，cloud agent 在下一课处理分配给它的议题时就会读取这些指令。

> [!TIP]
> 如果希望在本研讨会中直接使用 `main`，可以跳过分支步骤并直接提交到 `main`。此处创建分支是为了让研讨会流程贴近真实项目中的工作方式。

## 总结与后续步骤

你已了解 Copilot 如何获取本项目指令文件中的上下文，并向 `.github/copilot-instructions.md` 添加了一条适用于整个存储库的新标准。接下来几课中，cloud agent 创建的拉取请求会展示这条标准的作用。

接下来，将[第一个议题分配给 Copilot cloud agent][next-lesson]。

## 资源

- [用于自定义 GitHub Copilot 的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更优 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot — 指令文件和其他资源合集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
