---
title: "第 4 课 - 使用自定义指令引导 Copilot"
description: "查看存储库指令，添加文档规范，并将其应用于筛选功能代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

使用生成式 AI 时，上下文至关重要。如果任务有特定要求，就应让 Copilot 能够参考这些指导。[指令文件][instruction-files]不仅说明你想要什么代码，也说明代码应如何组织。现在筛选功能已完成，你将查看 Copilot 使用的指令、添加一项文档规范，并将其应用于代码。

本课将介绍如何：

- 了解存储库指令和按路径应用的指令文件如何提供给智能体。
- 更新指令文件，确保遵循编码规范。
- 查看指令文件对代码的影响。

## 场景

Tailspin Toys 有一套开发实践指南和要求，包括：

- 注释应解释意图和不明显的决策，而不是复述代码。
- `db/` 和 `src/lib/` 中导出的函数应使用 TSDoc/JSDoc 说明用途、参数和返回值；如果函数带有可注入的 `db` 参数，也应予以说明。
- 可复用的 Astro 组件应说明其 `Props` 接口；相关代码更改时，注释也应保持更新。
- 应保留现有格式和 lint 指南。

通过指令文件，你可以确保 Copilot 按照这些实践要求完成任务。

## 指令文件

自定义指令可以向 Copilot 提供上下文和偏好，帮助它理解你的编码风格和要求。你可以借此引导 Copilot 提供更相关的建议和代码片段，例如指定编码规范、库以及注释风格。指令既可以适用于整个存储库，也可以针对特定文件类型。

指令文件有两种：

- `.github/copilot-instructions.md`：每次针对该存储库的请求都会发送给 Copilot 的单个指令文件。内容应是大多数请求都适用的项目级信息。
- `.github/instructions/*.instructions.md`：针对特定语言、文件类型或任务提供指导的文件。

> [!NOTE]
> 其他指令格式及其支持情况会因工作环境而异。依赖特定格式前，请查看[自定义指令支持参考][custom-instructions-support]。

## 查看此项目的自定义指令文件

起始项目中已包含一些指令文件。先查看现有内容，再进行更改，以便了解其影响。

1. 返回 Codespace。
2. 在 Codespaces 编辑器中（而不是终端中）打开 `.github/copilot-instructions.md`。
3. 查看文件，留意其中的项目简介和编码指导。这些指令适用于 Copilot 在此存储库中的每次交互。
4. 打开 `.github/instructions` 文件夹并查看其中的文件。你会看到适用于 Astro 文件、Drizzle 数据层、测试等内容的指令。
5. 打开 `.github/instructions/unit-tests.instructions.md`。留意文件顶部的 `applyTo` 字段；其中的 glob 决定指令适用于哪些文件。
6. 打开 `.github/instructions/drizzle.instructions.md`，查看它指向其他指令文件和现有项目文件的链接。这样可以将较大的指令集拆分成较小、可复用的文件，并为 Copilot 提供可参考的示例。

## 更新指令文件以符合团队指南

现有文件是不错的起点，但仍有一项遗漏。现在修改核心的 `copilot-instructions.md` 文件，确保新生成的 TypeScript 代码包含 TSDoc 注释。

1. 在 `.github/copilot-instructions.md` 中找到 **Code formatting guidance** 部分，该部分应位于第 35 行附近。
2. 在该部分末尾添加以下项目：

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

文件会自动保存。

## 使用更新后的指导

Copilot CLI 会在对话启动时加载存储库指令。保存更新后的指令后，退出并恢复筛选功能对话，让 Copilot 在保留功能上下文的同时加载新指导。

1. 如果筛选功能对话仍处于打开状态，输入 `/exit` 关闭它。Copilot CLI 会自动保存对话。
2. 在存储库根目录的 `game-filters-cli` 分支上恢复已保存的对话：

   ```bash
   copilot --resume
   ```

   如果系统提示，请选择筛选功能对话，并确认当前检出的是 `game-filters-cli` 分支。
3. 请求 Copilot 应用更新后的指导：

   ```plaintext
   我们刚刚更新了指令和代码指导。请更新你生成的代码，使其符合这些指导。
   ```

4. 输入 `/diff`，阅读已更改的 TypeScript 文件。查看新生成的 TSDoc 注释，并确认它们准确说明了代码。

## 总结与后续步骤

你已了解 Copilot CLI 如何从指令文件获取上下文，并将新的规范应用于功能代码。具体来说，你：

- 了解了存储库指令和按路径应用的指令文件如何提供给智能体。
- 更新了指令文件，确保遵循编码规范。
- 查看了指令文件对代码的影响。

接下来，[自定义并运行可复用的 quality-checks 技能][next-lesson]，确保一致地运行 lint 和测试。

## 资源

- [为 Copilot CLI 添加自定义指令][instruction-files]
- [自定义指令支持][custom-instructions-support]
- [创建有效自定义指令的最佳实践][instructions-best-practices]
- [Awesome Copilot：指令文件和其他资源集合][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
