---
title: "第 3 课 - 智能体模式：Plan 和 Autopilot"
description: "使用 Plan 确定方案、使用 Autopilot 根据议题构建筛选功能，并在 Interactive 模式中审查结果。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

我们刚刚为项目添加了一项小功能。较大的更改则需要更稳妥的流程。GitHub Copilot CLI 可以配合组织现有的开发流程，帮助团队以正确的方式构建正确的功能。本课将开始一组典型的智能体开发练习：从议题出发生成新功能，确认代码有效、行为符合预期，最后成功合并到项目中。

> [!NOTE]
> 后续功能工作将沿用同一对话和分支。实际工作中，不同文件类型的更改通常会使用不同分支或 PR；本练习为了聚焦核心概念而简化了流程。

本课将介绍如何：

- 从 GitHub 议题启动新的 Copilot 对话。
- 在 Plan 模式中确定需求。
- 使用 Autopilot 模式实现新功能。
- 审查代码。
- 在转发的浏览器中手动验证功能。

继续开发该功能时，你还将更新存储库指令、自定义现有的 `quality-checks` 技能、添加 MCP 验证、创建 QA 智能体并创建功能 PR。

## 场景

Tailspin Toys 的目录不断扩大，访客需要按类别和发行商筛选游戏。待办议题描述了该功能，但组合类别等细节需要在编写代码前确定。你将使用 Plan 模式作出这些决定，再授权 Autopilot 在明确范围内实现功能。

## 背景

将 AI 编码智能体引入开发流程，并不会改变软件开发的基本原则；这些原则反而更重要。大多数开发人员遵循类似以下的流程：

1. 从已提交的议题开始，确认需要完成的工作。
2. 制定构建方案。
3. 编写并审查代码。
4. 运行测试以验证代码。
5. 手动验证新功能。
6. 创建拉取请求 (PR)。
7. 代码审查通过且持续集成 (CI) 成功后，合并代码。

> [!NOTE]
> 具体流程会因团队和组织而异，但大多与上述流程相似。

遵循这种标准流程，可以确保 AI 生成的代码符合需求，并经过与人工编写代码相同的审查流程。

## 对话模式

**对话模式**控制智能体的自主程度。按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 可在模式之间切换：

- **Interactive**：你与智能体协作。智能体提出更改建议，并等待你的输入后再继续。
- **Plan**：智能体先制定计划，但不能编辑项目文件。
- **Autopilot**：智能体自主工作，包括编写代码、运行测试并反复迭代，直至任务完成。

先在 Plan 模式中审查计划，然后使用 Autopilot 实现计划。

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

6. 按两次 <kbd>Tab</kbd> 打开 **Issues** 选项卡。
7. 按 <kbd>A</kbd> 显示所有议题。
8. 使用方向键选中标题为 **Allow users to filter games by category and publisher** 的议题。
9. 按 <kbd>C</kbd> 将议题添加到提示中，并返回 **Session** 选项卡。

请注意，提示现在以 `#7`（或类似编号）开头。`#` 可将 GitHub 上的议题或拉取请求 (PR) 添加到上下文中。

## 规划筛选功能

规划可以先明确功能或任务的实现方式，再交给 Copilot 处理。对于复杂工作，花些时间规划通常很有帮助。现在切换到 Plan 模式，让 Copilot 制定计划。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 切换到 Plan 模式。确认提示下方的模式指示器显示 **Plan**。
2. 在上一步添加的议题引用后输入以下提示：

   ```plaintext
   为实现此功能制定计划。
   ```

Copilot 会先探索项目，再确定合适的实现方案并整理计划。

3. Copilot 可能会询问筛选功能应如何工作。根据自己的偏好回答；这里没有唯一正确的答案。
4. 计划完成后，按 <kbd>Control</kbd>+<kbd>E</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>E</kbd>（Windows/Linux）展开计划。
5. 上下滚动审查计划。
6. 如果计划中的任何内容与你的决定不符，请要求 Copilot 修改。

## 批准 Autopilot

计划编写并审查完毕后，就可以开始实现。让 Copilot 使用 Autopilot 模式执行计划。

Autopilot 会让 Copilot 持续迭代，直到它认为任务已经完成。

1. 选择 **Accept plan and build on autopilot (recommended)**，或当前版本中含义相同的选项。
2. 确认提示下方的模式指示器显示 **Autopilot**。
3. 观察 Copilot 按计划迭代、生成代码并运行测试。

> [!NOTE]
> 批准后可能会立即开始实现，因此请先审查计划。如果 Copilot 报告缺少依赖项或端口冲突，请先解决设置问题，再将检查视为已完成。

## 审查并验证实现

代码生成后，和其他代码一样，必须在合并前进行审查。审查代码并运行网站，确认功能表现正常。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 进入 Interactive 模式。确认模式指示器不再显示 **Plan** 或 **Autopilot**。
2. 输入 `/diff`，检查筛选功能实现和测试。
3. 将结果与议题以及规划时作出的决定进行比较。
4. 审查代码后，按 <kbd>Esc</kbd> 退出差异视图。
5. 检查项目运行的检查结果，并要求 Copilot 修复失败项。

## 探索新功能

代码看起来没问题，但实际运行情况如何？像之前一样启动应用，通过 Codespaces 转发端口打开网站。

1. 让 Copilot 启动应用：

   ```plaintext
   启动应用，以便我在浏览器中试用筛选功能。告诉我 URL，并让服务器继续运行。
   ```

2. Codespaces 报告端口 `4321` 可用时，选择 **Open in Browser**。
3. 尝试按类别筛选、按发行商筛选，以及计划中确定的组合筛选。
4. 确认重置和无结果状态符合议题及你的决定。
5. 返回 Codespace，让 Copilot 停止它启动的开发服务器。

## 总结与后续步骤

你已使用不同的对话模式构建并审查功能。本课中，你：

- 从 GitHub 议题启动了新的 Copilot 对话。
- 在 Plan 模式中确定了需求。
- 使用 Autopilot 模式实现了新功能。
- 审查了代码。
- 在转发的浏览器中手动验证了功能。

接下来，[使用自定义指令][next-lesson]深入了解如何让代码遵循已记录的实践规范。

## 资源

- [GitHub Copilot CLI 中的 Autopilot][autopilot]
- [Copilot CLI 命令参考][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
