---
title: "练习 1 - 自定义指令（云智能体）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：先决条件][previous-lesson] · [下一课：Copilot 云智能体 →][next-lesson] |

使用生成式人工智能 (AI) 时，上下文至关重要。如果任务有特定要求，或者 Copilot 需要了解背景信息，就应确保它能够获取这些上下文。[指令文件][instruction-files]可以提供这些指导，让 Copilot 明白你不仅希望它做什么，也希望它如何完成任务。

本练习将介绍如何：

- 了解项目上下文、编码指南和文档规范如何通过存储库自定义指令及按路径应用的指令文件传递给 Copilot。
- 向 `.github/copilot-instructions.md` 添加新的存储库级标准。

> [!NOTE]
> 与 VS Code 和 CLI 工作环境不同，本练习不会比较提示执行前后的结果。Copilot 云智能体会异步处理 GitHub 议题，因此难以实时并排展示指令的影响。稍后审查云智能体创建的拉取请求时，你会看到指令文件发挥的作用。

## 指令文件

### 场景

Tailspin Toys 有一套开发实践指南和要求，包括：

- 数据层始终需要单元测试。
- 用户界面应采用深色模式，并呈现现代风格。
- 应以 TSDoc 文档注释的形式为代码添加文档。
- 每个文件开头都应添加注释块，说明文件的用途。

使用指令文件，可以确保 Copilot 依据这些实践要求完成任务。

### 自定义指令

自定义指令可以向 Copilot 提供上下文和偏好，帮助它理解你的编码风格和要求。你可以借此引导 Copilot 提供更相关的建议和代码片段，例如指定编码规范、库以及注释风格。指令既可以适用于整个存储库，也可以针对特定任务的文件类型。

指令文件有两种：

- `.github/copilot-instructions.md`：每次针对该存储库的请求都会发送给 Copilot 的单个指令文件。内容应是大多数聊天或 CLI 请求都适用的项目级信息，例如所用技术栈、项目概述、最佳实践和其他通用指导。
- `.github/instructions/*.instructions.md`：可针对特定任务或文件类型创建这些文件。例如，为 TypeScript 或 Astro 等语言提供指导，或为创建用户界面组件和单元测试等任务提供指导。

> [!NOTE]
> 在集成开发环境 (IDE) 中，这些指令文件只用于 Copilot Chat 生成代码，不用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体在生成代码时都会使用存储库级指令文件以及带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> Copilot 还[支持其他规范的指令文件][custom-instructions-support]，包括 AGENTS.md 和 CLAUDE.md 文件。

### 管理指令文件的最佳实践

本工作坊不会深入讲解如何编写指令文件，不过示例项目展示了一种常见做法。总体而言：

- 将 `copilot-instructions.md` 中的指导限定在项目级内容，例如项目用途、结构和全局编码规范。
- 使用 `*.instructions.md` 文件为特定文件类型（如单元测试、Astro 组件和数据层）或特定任务提供指导。
- 使用自然语言，保持指导清晰，并提供代码应如何编写或不应如何编写的示例。

编写指令文件没有唯一正确的方法，使用 AI 也是如此。通过试验找到最适合项目的做法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应有一套完善的指令文件。查看本项目中的文件时，你会发现其中包括适用于[用户界面更新][ui-instructions]和 [Astro][astro-instructions] 等任务的指令。
>
> Copilot 也可以协助生成指令文件。不同产品界面的操作方式有所不同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。对应产品的课程会在相关处介绍操作方法。
>
> 如需模板或起点，可查看 [awesome-copilot][awesome-copilot]，其中收录了指令文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 查看此项目的自定义指令文件

先阅读存储库中已有的指令文件。项目包含一个核心 `copilot-instructions.md` 文件，以及一组适用于不同任务的 `*.instructions.md` 文件。你可以在编辑器或 GitHub 网站界面中打开这些文件。

1. 打开 `.github/copilot-instructions.md`。
2. 查看项目简介，以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。特别留意 **Code standards** 下的 **GitHub Actions Workflows** 指导。这些内容适用于你与 Copilot 的各种交互。
3. 打开 `.github/instructions` 文件夹并查看其中的文件。你会看到适用于 Astro 文件、Drizzle 数据层、测试等内容的指令。
4. 打开 `.github/instructions/unit-tests.instructions.md`。留意文件顶部的 `applyTo` frontmatter；其中的 glob 相对于存储库根目录，用于指定指令适用的文件。这里，任何 TypeScript 测试文件（例如匹配 `**/*.test.ts` 的文件）都符合条件。
5. 查看此项目用于创建单元测试的专门指令。
6. 最后，打开 `.github/instructions/drizzle.instructions.md` 并滚动到文件底部。留意它指向其他指令文件（例如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将较大的指令集拆分成较小、可复用的文件，并为 Copilot 提供示例。这里的路径相对于指令文件所在位置，而不是存储库根目录。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分记录了项目编码规范，但尚未要求为代码添加文档注释。接下来会添加 TSDoc 文档注释和文件注释头的规则。

## 添加新的存储库标准

接下来只需编辑一次文件：添加适用于整个项目的规则，要求在代码中使用 TSDoc 文档注释和文件级注释头。后续练习中，云智能体处理议题时会读取这项规则。

编辑前先创建分支。云智能体会从议题目标分支读取指令，但仍建议单独提交这项更改：

1. 在 Codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

如前所述，`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。现在添加编码规范，提高代码建议的质量。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分，该部分应位于第 27 行附近。查看其中记录的项目编码规范；目前尚无代码文档规则，因此生成的辅助函数没有文档注释。
3. 在现有规范下方添加以下 Markdown 内容，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 如前一课所述，指令文件可以放在存储库级别的 `.github/copilot-instructions.md` 中，提供全局指导；也可以放在 `*.instructions.md` 文件中，针对特定语言、文件类型或任务提供指导。你刚添加的文档注释规则属于项目级规范，因此适合写入存储库级文件。

## 提交、推送并合并指令更新

云智能体会读取议题目标分支中的指令。下一练习将把议题分配给 Copilot，届时它会从 `main` 分支创建新分支，因此必须先将指令更改合并到 `main`，云智能体才能读取。

1. 暂存并提交更改：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 到 `main` 的拉取请求并合并。下一练习中，云智能体处理议题时就会读取这些指令。

> [!TIP]
> 如果本工作坊中希望直接在 `main` 上操作，可以跳过创建分支，直接提交到 `main`。此处采用分支，是为了模拟真实项目中的工作方式。

## 总结与后续步骤

你已了解 Copilot 如何从项目指令文件获取上下文，并在 `.github/copilot-instructions.md` 中添加了新的存储库级标准。后续练习中，可以在云智能体创建的拉取请求里看到这项规范的效果。

接下来，[将首个议题分配给 Copilot 云智能体][next-lesson]。

## 资源

- [用于自定义 GitHub Copilot 的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更有效 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot：指令文件和其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
