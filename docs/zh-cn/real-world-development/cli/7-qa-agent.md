---
title: "第 7 课 - 创建并使用质量保证智能体"
description: "创建质量保证 (QA) 自定义智能体，将议题需求、quality-checks 技能和 Playwright MCP 结合起来。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

你已使用 `quality-checks` 技能运行自动检查，并通过 Playwright MCP 在浏览器中观察筛选功能。现在将这些能力整合到自定义智能体中，并为它定义清晰的质量保证 (QA) 流程。

本课将介绍如何：

- 了解自定义智能体如何结合指令、技能和 MCP 工具。
- 创建并检查可复用的质量保证配置文件。
- 选择 QA 智能体，并根据筛选议题审查其结果。

## 场景

Tailspin Toys 希望在创建拉取请求 (PR) 前，使用统一流程审查需求、代码质量、自动检查、测试覆盖率和浏览器行为。自定义智能体可以协调这一质量保证流程，并生成可复用的报告。

## 什么是自定义智能体？

自定义智能体是通过 Markdown 配置文件定义的 Copilot 专用版本。配置文件说明智能体的用途、指令和可用工具。本工作坊将在 `.github/agents/qa.agent.md` 中定义质量保证角色，并在 Copilot CLI 中选择该智能体。

你使用的自定义项各有不同用途：存储库指令说明团队标准；`quality-checks` 技能封装可重复执行的检查；Playwright MCP 提供浏览器工具；QA 配置文件则指导 Copilot 如何使用这些能力评估需求并报告发现。配置文件不会取代这些功能，也不需要另开对话。

## 创建 QA 配置文件

创建功能 PR 前，让 Copilot 创建一个可复用的 QA 配置文件。配置文件应明确 QA 要执行的检查和必须遵守的边界。

1. 返回 Codespace，确认筛选功能对话处于 Interactive 模式。
2. 让默认智能体创建新的自定义智能体：

   ```plaintext
   在 .github/agents/qa.agent.md 中创建名为 QA 的自定义智能体。它应根据议题和已商定的需求检查功能，遵循存储库指令，运行 quality-checks 技能，使用 Playwright MCP 验证行为，并在测试覆盖不足时添加测试。

   它应将每项需求标记为通过、失败或受阻，并提供支持证据。修改实现代码前必须先询问我，且不得提交更改或创建拉取请求。

   现在只创建配置文件，以便我审查。
   ```

## 检查配置文件

使用新智能体前，先审查其配置文件，确认 Copilot 正确记录了 QA 工作流和边界。这样可避免配置不完整或权限过宽的智能体在你只想验证功能时擅自更改代码。

1. 输入 `/diff`，打开 `.github/agents/qa.agent.md`。
2. 阅读 frontmatter。`description` 为必填项；`name` 是可选项，但添加后能为智能体提供明确的显示名称。
3. 阅读配置文件中的指令，确认 QA 会从需求出发、遵循存储库指令、运行 `quality-checks` 技能并使用 Playwright MCP。
4. 确认 QA 会提供支持证据、修改实现代码前会先询问，并且不会提交更改或创建拉取请求。
5. 如果生成的配置文件遗漏了任何职责或边界，请先让默认智能体修改，再继续。

## 根据议题运行 QA

Copilot CLI 会在对话启动时加载项目智能体。创建配置文件后，恢复同一筛选功能对话并选择 QA，使它能够使用已有的议题和规划决策。

1. 输入以下提示启用智能体：

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 由于刚创建智能体，它可能暂时不会显示在可用智能体列表中。不过该命令仍会启用它。

2. 使用以下提示让 QA 智能体审查功能：

   ```plaintext
   根据议题和计划中确定的事项审查筛选功能。它可以准备好创建 PR 了吗？
   ```

3. 等待 QA 智能体完成工作。
4. 阅读它生成的报告。

## 总结与后续步骤

你已为工作流添加可复用的专家角色，并审查了它的工作。本课中，你：

- 了解了自定义智能体如何结合指令、技能和 MCP 工具。
- 创建并检查了可复用的质量保证配置文件。
- 选择了 QA 智能体，并根据筛选议题审查了其结果。

现在，实现、技能更新、QA 配置文件、测试和验证报告都已准备好接受审查。接下来，[将这些内容整合到功能 PR 中，并使用 Agent Merge][next-lesson]。

## 资源

- [为 Copilot CLI 创建自定义智能体][create-agents]
- [自定义智能体配置][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
