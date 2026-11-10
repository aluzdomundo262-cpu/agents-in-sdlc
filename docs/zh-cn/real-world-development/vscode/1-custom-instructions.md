---
title: "练习 1 - 自定义指令（VS Code）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：智能体模式 →][next-lesson]

使用生成式人工智能 (AI) 时，上下文至关重要。如果任务有特定要求，或者 Copilot 需要了解背景信息，就应确保它能够获取这些上下文。你可以通过多种方式向 Copilot 提供具体上下文，其中一种重要方式是使用[指令文件][instruction-files]指导代码生成。

本练习将介绍如何：

- 了解项目上下文、编码指南和文档规范如何通过存储库自定义指令及按路径应用的指令文件传递给 Copilot。
- 使用当前指令生成筛选功能的第一个数据切片（发行商辅助函数）。
- 向 `.github/copilot-instructions.md` 添加新的存储库级标准。
- 再次运行相同提示，观察生成的代码如何遵循新标准。
- 将指令更新和筛选功能切片提交到 `main`，以便 Copilot 在下一练习中使用更新后的指导。

> [!CAUTION]
> 生成的代码可能不符合所有自定义规范。Copilot 的输出具有概率性。本练习旨在观察更新指令前后行为的**趋势**变化，而不是要求输出逐字相同。

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
4. 打开 `.github/instructions/unit-tests.instructions.md`。留意文件顶部的 `applyTo` 字段；其中的 glob 相对于存储库根目录，用于指定指令适用的文件。这里，任何 TypeScript 测试文件（例如匹配 `**/*.test.ts` 的文件）都符合条件。
5. 查看此项目用于创建单元测试的专门指令。
6. 最后，打开 `.github/instructions/drizzle.instructions.md` 并滚动到文件底部。留意它指向其他指令文件（例如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将较大的指令集拆分成较小、可复用的文件，并为 Copilot 提供示例。这里的路径相对于指令文件所在位置，而不是存储库根目录。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分记录了项目编码规范，但尚未要求为代码添加文档注释。接下来会添加 TSDoc 文档注释和文件注释头的规则。

## 为更改创建分支

按照最佳实践，为本次更改创建一个分支。

1. 从上一练习返回 Codespace。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新的终端。
3. 创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions
   ```

## 更新指令前先使用 Copilot Chat

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。不同练习所用的模式和模型可能不同；相关步骤会在需要时说明。

要查看自定义指令的影响，先在当前指令文件不变的情况下发送提示。稍后更新指令文件后，再发送相同提示并比较结果。

1. 关闭之前练习中打开的编辑器选项卡，避免 Copilot 获取不需要的上下文。
2. 打开 `src/lib/publishers.ts`，让 Copilot 知道辅助函数应放在哪里。
3. 在 Chat 视图的智能体下拉列表中选择 **Agent**，让 Copilot 可以修改文件。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

4. 发送以下提示：

   ```plaintext
   创建或更新 src/lib/publishers.ts，添加一个数据访问辅助函数，返回所有发行商的名称和 ID 列表。应用文件更改。
   ```

5. Copilot 会探索项目并应用代码更改，通常会同时修改辅助函数文件和测试。
6. 留意建议的辅助函数是一个带类型的函数：它将 `db` 客户端作为第一个参数，并返回带类型的发行商数组。这些做法来自 `.github/instructions/drizzle.instructions.md` 中适用于 `src/lib/*.ts` 的数据层规范。
7. 留意建议的代码**缺少** TSDoc 文档注释和文件级注释头。

> [!CAUTION]
> Copilot 的输出具有概率性，因此它也可能在没有明确指示时添加文档注释。如果出现这种情况也没关系；本练习关注的是更新指令后行为是否更加一致。

## 添加新的存储库标准

如前所述，`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。现在添加一项编码标准，提高代码建议的质量。

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

## 重新发送提示并观察更改

1. 返回 Copilot Chat 并选择 **New Chat**，清空对话内容。
2. 再次选择 `src/lib/publishers.ts`，让 Copilot 关注正确的文件。
3. 发送与之前**相同的提示**：

   ```plaintext
   创建或更新 src/lib/publishers.ts，添加一个数据访问辅助函数，返回所有发行商的名称和 ID 列表。应用文件更改。
   ```

4. 留意建议的文件现在以类似以下注释块开头：

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. 留意建议的函数现在包含类似以下的 TSDoc 注释：

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

你已引导 Copilot 遵循新的项目规范，并将其应用于真实代码。下一练习将在此基础上继续构建。

## 提交指令并推送分支

指令文件和存储库中的其他资源一样，也需要通过源代码管理进行维护。现在提交并推送分支。

1. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新的终端。
2. 在终端中运行以下命令，确认指令和辅助函数更改已存在：

   ```bash
   git status
   ```

3. 在终端中暂存指令更新和 Copilot 为辅助函数基础所做的所有更改，并提交：

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # 如果 git status 显示还有其他相关更改（例如测试），也将这些文件加入暂存区。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. 在终端中将分支推送到存储库：

   ```bash
   git push -u origin custom-instructions
   ```

## 创建并合并拉取请求

分支推送完成后，创建拉取请求 (PR)，并关联待办事项中的文档规范议题。也可以让 Copilot 使用已连接到项目的 GitHub 工具代为处理：查找议题、创建用于关闭该议题的 PR，然后合并。

> [!NOTE]
> 这是第一次让 Copilot 代表你操作 GitHub。项目模板已将 GitHub 工具连接到工作区，因此无需额外配置。Copilot 首次使用工具时，VS Code 可能会提示你登录 GitHub。按提示授权即可。后续练习会通过模型上下文协议 (MCP) 介绍这种连接方式。

1. 在 Codespace 中打开 Copilot Chat。
2. 按 <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd>（Windows/Linux）打开 Copilot Chat 视图，并确认智能体选择器中已选中 **Agent**。
3. 让 Copilot 查找与更新指令文件相关的议题，并从当前分支创建 PR，说明指令更新和为后续筛选工作添加的发行商辅助函数基础：

   ```plaintext
   查找与更新指令文件相关的议题。从当前分支创建新的 PR，并说明该 PR 会关闭此议题；还要说明我们为后续筛选功能添加了发行商辅助函数基础。
   ```

4. Copilot 会查找议题并创建 PR。
5. Copilot 请求你**Allow**代为执行 GitHub 操作时，先审查操作，再根据情况选择 **Allow**。
6. PR 创建后，让 Copilot 合并 PR，并将本地分支切回 `main`：

   ```plaintext
   将 PR 合并到 main。然后在本地切回 main 并拉取最新代码，确保代码已更新。
   ```

7. Copilot 请求你**Allow**代为执行 GitHub 操作和 shell 命令时，先审查操作，再根据情况选择 **Allow**。

现在，你已借助 GitHub Copilot 创建并合并了拉取请求。

## 总结与后续步骤

本练习中，你：

- 了解了项目上下文、编码指南和文档规范如何通过存储库自定义指令及按路径应用的指令文件传递给 Copilot。
- 使用代码生成提示，并观察现有指令下 Copilot 生成的内容。
- 向 `.github/copilot-instructions.md` 添加新的存储库级标准。
- 再次发送相同提示，观察建议的代码如何遵循新标准。
- 将指令更新和辅助函数基础提交到 `main`，供下一练习使用。

接下来，在[智能体模式][next-lesson]中应用这些指令，让 Copilot 跨代码库添加新功能。

## 资源

- [用于自定义 GitHub Copilot 的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更有效 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [GitHub Copilot 个人自定义指令][personal-instructions]
- [Awesome Copilot：指令文件和其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
