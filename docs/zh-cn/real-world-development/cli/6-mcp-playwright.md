---
title: "第 6 课 - 使用 Playwright MCP 验证功能"
description: "在 Copilot CLI 中检查或配置 Playwright MCP，并让它通过浏览器探索筛选功能。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

编写代码只是开发工作的一部分。我们还要处理数据和外部服务，并让 Copilot 使用其他自动化工具。这时就需要模型上下文协议 (MCP) 服务器。MCP 服务器可以扩展 Copilot CLI 的内置功能，为它提供更多工具和服务。

本课将介绍如何：

- 了解 MCP 的含义以及 Copilot CLI 如何使用它。
- 在尚未配置时添加 Playwright MCP 服务器。
- 让智能体操作浏览器并探索筛选功能。

## 场景

单元测试和端到端测试固然重要，但要验证用户界面更新，还需要实际与界面交互。你将允许 Copilot 像用户一样使用正在开发的网站，从而自动检查更改，并提高对功能行为的信心。

## 什么是模型上下文协议 (MCP)？

[模型上下文协议 (MCP)][mcp-blog-post] 为人工智能 (AI) 智能体提供了与外部工具和服务通信的方式。通过 MCP，AI 智能体可以实时访问外部工具和服务，获取最新信息并代表你执行操作。

智能体通过 MCP 服务器访问这些工具和资源。MCP 服务器充当 AI 智能体与外部工具和服务之间的桥梁。每个 MCP 服务器都提供一组智能体可以访问的工具和资源。

常见的 MCP 服务器包括：

- **[GitHub MCP Server][github-mcp]**：提供用于管理 GitHub 存储库、议题和拉取请求的 API。
- **[Playwright MCP Server][playwright-mcp-server]**：使用 Playwright 提供浏览器自动化功能。

MCP 服务器还有很多。GitHub 提供了 [MCP 注册表][mcp-registry]，帮助开发者发现资源并为生态系统做出贡献。

> [!CAUTION]
> 对待 MCP 服务器应像对待项目中的其他依赖项一样。使用前请审查其源代码、验证发布者，并考虑相关安全影响。

## 添加 Playwright MCP 服务器

如果尚未配置 Playwright MCP 服务器，请添加它，以便 Copilot 像用户一样与网站交互。

> [!NOTE]
> 如果 Copilot CLI 中已配置 Playwright MCP，请跳过这些设置步骤，直接继续下一节。

1. 返回 Codespace。
2. 在 Copilot CLI 中输入以下命令，打开添加 MCP 服务器的对话框：

   ```plaintext
   /mcp add
   ```

3. 在名称字段中输入 `playwright`，然后按 <kbd>Tab</kbd>。
4. 按 <kbd>Enter</kbd> 确认服务器类型为 **STDIO**，然后按 <kbd>Tab</kbd>。
5. 在 **Command** 对话框中粘贴以下命令：

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. 按 <kbd>Control</kbd>+<kbd>S</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>S</kbd>（Windows/Linux），保存新 MCP 服务器。
7. 按 <kbd>Esc</kbd> 退出 MCP 对话框。

## 让 Copilot 使用 Playwright 探索功能

之前你已手动确认功能行为正常。现在使用 Copilot 中的 Playwright MCP 服务器执行同样的检查。

1. 使用以下提示，让 Copilot 通过 Playwright MCP 验证功能：

   ```plaintext
   启动应用，并使用 Playwright MCP 按照议题和我们的计划检查筛选功能。告诉我哪些功能正常、哪些不正常，但不要进行任何更改。完成后停止你启动的服务器。
   ```

> [!NOTE]
> 你不一定需要明确要求 Copilot 使用 MCP 服务器，它通常会自行判断。不过，明确指出所需工具有助于获得更一致的结果，也能减少一些令牌消耗。

2. 观察 Copilot 列出它在浏览器中执行的步骤，以确认功能是否正常。
3. 阅读报告，确认所有行为符合预期。

Copilot 会启动服务器，使用 Playwright 操作网站，停止服务器，并向你提供报告。

## 总结与后续步骤

恭喜，你已通过 Copilot CLI 中的 Playwright MCP 服务器，在真实浏览器中探索功能。本课中，你：

- 了解了 MCP 的含义以及 Copilot CLI 如何使用它。
- 在尚未配置时添加了 Playwright MCP 服务器。
- 让智能体操作浏览器并探索了筛选功能。

接下来，创建一个[质量保证 (QA) 自定义智能体][next-lesson]，将技能和浏览器工具整合到专门的角色中。

## 资源

- [MCP 是什么，为什么大家都在讨论它？][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [向 Copilot CLI 添加 MCP 服务器][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
