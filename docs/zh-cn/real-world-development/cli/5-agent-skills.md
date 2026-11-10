---
title: "练习 5 - 自定义并使用 quality-checks 技能"
description: "了解现有的 quality-checks 技能，自定义其报告格式，然后重新加载并运行该技能。"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

编写代码只是开发工作的一部分。此前，你已经手动验证代码是否正常运行，并使用说明文件确保代码符合规范。接下来还要考虑测试、代码检查，以及持续集成（CI）的其他环节。

**智能体技能**适合执行这类任务！技能可以帮助 Copilot 了解如何正确运行这些操作。

在本练习中，你将：

- 探索现有的 `quality-checks` 技能。
- 自定义结果的报告格式。
- 重新加载并运行该技能。

## 场景

Tailspin Toys 使用 `quality-checks` 技能运行单元测试、代码检查和类型检查。团队希望改进报告，让结果更易于阅读。

## 说明、脚本和资源

智能体技能会打包可重复使用的任务说明、可执行脚本和辅助资源，供智能体按需加载。技能的核心是一个以技能名称命名的文件夹，其中包含名为 `SKILL.md` 的 Markdown 文件。该文件的 frontmatter 包含 `name` 和 `description`，用于定义技能的用途；正文介绍技能的功能以及何时调用它。文件夹中还可以包含供技能使用的脚本和其他资源子目录。

> [!NOTE]
> 技能不一定需要额外的文件或文件夹。Tailspin Toys 的 `quality-checks` 技能只包含 `SKILL.md`，因为它使用项目中已有的命令。

技能可以放在项目的 `.github/skills` 文件夹中，作为团队共享和复用的存储库资源；也可以放在用户技能文件夹 `~/.copilot/skills` 中。

## 探索技能

接下来查看 Tailspin Toys 团队用于运行单元测试、代码检查和类型检查的 `quality-checks` 技能。

1. 返回 Codespace。在 Codespaces 编辑器中打开 `.github/skills/quality-checks/SKILL.md`。
2. 阅读文件顶部的 `name` 和 `description`。description 可帮助 Copilot 判断何时调用该技能。
3. 阅读说明，留意它们如何引导 Copilot 完成测试和代码检查。
4. 注意该技能目前没有 **Results output formatting** 部分。

## 修改前先运行技能

技能可以直接通过 Copilot CLI 调用，也可以使用自然语言调用。现在让 Copilot 运行该技能中的三项检查。

1. 返回筛选功能的 Interactive 模式对话。
2. 输入以下提示：

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 记下最后生成的报告。

## 自定义报告

现在改进报告，使其说明运行了哪些检查、检查是否成功，以及工具实际报告了什么。你将更新技能，让它生成这样的报告。

1. 返回 `.github/skills/quality-checks/SKILL.md`。
2. 在文件末尾添加以下部分：

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. 文件会自动保存。

## 运行更新后的技能

修改完成后，查看新报告的效果。Copilot CLI 无需重启对话即可重新加载已编辑的技能。

1. 输入：

   ```plaintext
   /skills reload
   ```

2. 输入与之前完全相同的提示：

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 记下最后生成的报告，并与第一次的报告比较。

## 总结和后续步骤

在本练习中，你探索了用于单元测试、代码检查和类型检查的 `quality-checks` 技能，自定义了结果报告格式，并重新加载和运行了该技能。

这项更改将与筛选功能一起纳入功能拉取请求（PR）。接下来，你将通过 [Playwright MCP 服务器][next-lesson]让 Copilot 直接与网站交互。

## 更多技能示例

以下社区示例仅供参考，不是额外的练习任务：

- [Agent Skills 规范][skill-spec]
- [贡献工作流：`make-repo-contribution`][contribution-example]
- [需求文档：`prd`][prd-example]
- [图表及其打包的导出脚本：`drawio`][drawio-example]
- [浏览器测试：`webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
