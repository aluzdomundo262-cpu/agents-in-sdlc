---
title: "练习 2 - 使用 Copilot 智能体模式添加功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

即使是最简单的应用更新，通常也需要修改多个文件并执行测试等操作。开发人员往往需要找出所有相关文件、进行修改、运行测试、调试、找出遗漏的文件，再次修改……工作会不断重复。

Copilot 智能体模式正是为此而设计的。

Copilot 智能体模式可以在集成开发环境 (IDE) 中更自主地工作。它会像开发人员一样探索现有项目结构、执行必要的更新、运行测试等任务，并自动修复发现的问题。现在看看如何使用智能体模式为网站添加新功能。

> [!NOTE]
> 智能体模式和云智能体的名称相似，但适用于不同的工作方式。智能体模式在 IDE 中执行任务，便于快速反馈和交互。云智能体则像团队中的同事一样异步工作，通过议题和拉取请求与你协作。

本练习将介绍如何：

- 让 Copilot 智能体模式探索项目、识别相关文件并协调更改。
- 使用 GitHub Copilot 智能体模式跨用户界面 (UI) 和数据层实现新功能。
- 在将代码合并到代码库之前，审查 Copilot 智能体模式生成的更改和测试。

## 场景

随着游戏列表不断扩大，你希望允许用户按类别和发行商筛选。上一练习已添加发行商辅助函数，现在将使用 Copilot 智能体模式完成剩余的数据层、用户界面和测试工作。

## 运行 Tailspin Toys 网站

修改代码前，先浏览 Tailspin Toys 网站，了解它目前的功能。

该网站是一个以开发者为主题的桌游众筹平台，可列出游戏并显示游戏详情。整个网站是一个 Astro 应用，会在构建时将页面渲染为静态超文本标记语言 (HTML)。页面通过 Drizzle 对象关系映射器 (ORM)，在 frontmatter 中直接查询本地 SQLite 数据库。项目没有单独的后端应用程序编程接口 (API) 或客户端用户界面框架。可复用的数据访问辅助函数位于 `src/lib/`，交互功能则通过范围有限、使用标准文档对象模型 (DOM) API 的 Astro `<script>` 实现。

### 启动网站

项目提供了 `npm run dev` 任务，用于启动单个 Astro 开发服务器。按以下步骤在 GitHub Codespace 中运行网站：

1. 返回 Codespace。上一练习结束后，你应已切回 `main`。
2. 在 Codespace 中按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux）打开新终端。
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

   Astro 开发服务器准备就绪后，会显示类似以下内容的横幅：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> 如果弹出对话框，询问是否要为 `http://localhost:4321` 打开浏览器窗口，请选择 **x** 将其关闭。

5. 在终端中按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），然后选择 Astro 服务器地址 `http://localhost:4321`，打开网站。

> [!NOTE]
> 在 Codespace 中选择终端里的 localhost 链接时，系统会自动将你转到 `https://<your-codespace-name>-4321.app.github.dev/`。这是一个通往 Codespace 的私有隧道，Web 服务器目前就在其中运行。

### 浏览网站

网站运行后，先查看其现有功能：

- **主页**：显示游戏列表，包括标题、图片和描述。
- **游戏详情页**：选择游戏后会打开详情页，显示标题、描述、发行商和类别等信息。

## 使用 Copilot 探索待办事项

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。不同练习所用的模式和模型可能不同；相关步骤会在需要时说明。

网站初始版本可以正常运行，但我们希望添加新功能。先查看待办事项。通过模板创建项目时，系统已自动生成一组议题；让 GitHub Copilot 显示这些议题。

1. 在 Chat 视图的智能体下拉列表中选择 **Agent**。该智能体可以自主规划并跨文件实现更改、运行终端命令和调用工具。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

2. 从可用模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 本工作坊作者并非推荐某个模型。编写本工作坊时使用了 Claude Sonnet 4.5，因此在步骤中列出它，希望帮助你获得相对一致的体验。不过，大型语言模型 (LLM) 的输出具有概率性，因此建议可能与本工作坊中的示例不同。这是正常情况。

> [!NOTE]
> 由于 LLM 的概率性，Copilot 可能会使用不同的模型上下文协议 (MCP) 命令，但仍应能完成任务。

3. 发送以下提示，让 Copilot 查看议题待办事项：

   ```plaintext
   请显示我 GitHub 存储库中的待办事项，并根据对用户最有用的程度帮助我确定优先级。
   ```

4. 选择 **Continue**，运行列出所有议题的命令。
5. 查看生成的议题列表。

留意 Copilot 还会根据它认为对用户最有用的程度为待办事项排序。

## 查看指令文件

让智能体生成代码前，先查看用于提供工作上下文的指令文件。本练习将使用[用户界面指令文件](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)，了解如何为网站添加功能。

1. 在 Codespace 中打开 `.github/instructions/ui.instructions.md`。
2. 查看添加功能时的总体指导，包括：
   - 架构概述。
   - 组件设计、可测试性和无障碍原则。
   - 指向不同文件类型专用指令的链接，包括：
     - Astro。
     - Tailwind 层叠样式表 (CSS)。
     - Drizzle。

> [!TIP]
> 指令文件可以链接到其他指令文件和项目文件。路径相对于指令文件所在位置。这样可以复用指令、将复杂内容拆分成较小部分，并提供示例和模板。

## 实现筛选功能

完成筛选功能至少需要更新应用的三个部分：

- 添加或完善数据层 (`src/lib/`) 中剩余的筛选逻辑。
- 添加或更新筛选行为测试。
- 更新游戏列表页，添加筛选用户界面。

此外，合并前必须运行并通过测试。Copilot 智能体模式可以帮助完成这些任务。

1. 可以继续使用当前 Copilot 对话，也可以选择 **New Chat** 开始新对话。
2. 选择 **Add Context**、**Instructions**，然后选择 `ui` 指令文件。

   ![选择 UI 指令文件的示例](../../../_images/ex3-select-instructions-file.png)

3. 确认 Chat 视图的智能体下拉列表中仍选中 **Agent**。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

4. 确认仍选择 **Claude Sonnet 4.5** 模型。
5. 使用以下提示，让 Copilot 根据待办事项中的相关议题实现功能：

   ```plaintext
   请根据待办事项中相关 GitHub 议题的要求，更新网站以支持按发行商和类别筛选。上一练习已添加发行商辅助函数；完成剩余的数据层、用户界面和测试工作时，请保留并按需完善该实现。完成前确保所有测试通过。服务器已在运行，无需重新启动。
   ```

6. 观察 Copilot 探索项目并查找相关文件。它应会找到数据层辅助函数、用户界面和测试，之后修改文件并运行测试。

   ![Copilot 正在探索项目文件](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot 会执行多个步骤，例如探索项目、修改文件和运行测试。根据任务和代码库的复杂度，这可能需要几分钟。过程中，代码编辑器可能会显示 **Keep** 和 **Undo**。Copilot 完成后，每项更改都会提供 **Keep** 或 **Undo** 选项；工作尚未完成时无需选择。

7. Copilot 提示运行测试时，选择 **Continue**。

   ![Copilot Chat 提示是否允许运行测试](../../../_images/ex3-agent-mode-run-tests.png)

8. Copilot 可能会暂停一段时间，测试过程中也可能出现失败。这是正常的。Copilot 会在生成代码和运行测试之间迭代，直到任务完成且未发现错误。

   ![已完成的 Copilot 智能体模式 Chat 会话](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 检查生成的代码，留意潜在问题。

> [!CAUTION]
> 务必审查 Copilot 或其他 AI 工具生成的代码。

10. 返回正在运行网站的浏览器，试用新功能。
11. 确认功能正常并审查代码后，在 Copilot Chat 窗口中选择 **Keep**。

## 总结与后续步骤

恭喜，你已使用 GitHub Copilot 智能体模式为 Tailspin Toys 网站添加功能。本练习中，你了解了如何：

- 让 Copilot 智能体模式探索项目、识别相关文件并协调更改。
- 使用 GitHub Copilot 智能体模式跨用户界面和数据层实现新功能。
- 在将代码合并到代码库之前，审查 Copilot 智能体模式生成的更改和测试。

接下来，使用 [Playwright MCP 服务器测试功能][next-lesson]，并为其创建拉取请求。

### 额外探索练习 — 实现分页

随着游戏列表增长，网站将需要分页。运用本练习学到的技能，让 Copilot 更新网站以实现分页。编写提示时可以考虑：

- 遵循现有最佳实践，包括使用已有的指令文件。
- 决定分页的实现方式，例如是否允许用户选择每页条目数，还是使用固定数量。
- 在提示中提供必要的指导，帮助 Copilot 按照你的预期实现功能。
- 按需与 GitHub Copilot 迭代，提出更改请求并补充上下文。这是正常的协作流程。

## 资源

- [Copilot ask、edit 和 agent 模式：功能与适用时机][choose-mode]
- [VS Code 中的智能体模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
