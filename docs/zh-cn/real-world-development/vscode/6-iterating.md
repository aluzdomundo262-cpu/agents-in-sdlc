---
title: "练习 6 - 迭代改进 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
next: false
---

| [← 上一课：监控和管理智能体][previous-lesson] |
| :-- |

## 审查工作

在本实验中，你与 GitHub Copilot 合作完成了多项改善用户体验的任务：使用代理模式在客户端和服务器端添加筛选功能，通过模型上下文协议（MCP）服务器在浏览器中手动测试，然后使用自定义智能体实现无障碍功能，包括高对比度和浅色模式切换，并在会话进行中引导智能体扩展工作。现在，你将发布本地更改，并按照团队的方式进行审查。

### 场景

加入生成式人工智能（AI）并不会改变软件设计和开发运维（DevOps）的基本原则。Copilot 生成的成果仍需要经过正式审查。因此，接下来将把 Codespace 中的无障碍更改推送到分支、创建拉取请求，并在邀请团队其他成员参与前检查差异。

## 发布无障碍功能

你在[练习 4][exercise-4]和[练习 5][exercise-5]中使用无障碍自定义智能体实现的高对比度和浅色模式切换功能，已经作为提交保存在 Codespace 中。接下来，将这些更改推送到分支并创建拉取请求（PR），供团队审查。

1. 返回 Codespace。
2. 在 VS Code 中打开 **Source Control** 视图。
3. 确认无障碍更改已提交。如果练习 5 中还有未提交的更改，现在将其暂存并提交，使用描述性消息，例如 `Add high-contrast and light-mode toggles`。
4. 选择 **Publish Branch** 发布分支，或使用 **...** 菜单中的 **Push**。
5. VS Code 会提示你在 github.com 上打开新分支。接受提示，或手动前往存储库，在分支横幅上选择 **Compare & pull request**。
6. 设置清晰的标题（例如 `Add high-contrast and light-mode toggles`），并用简短说明概括所做的更改及其原因。
7. 选择 **Create pull request**。
8. 创建 PR 后，选择 **Files changed** 选项卡，端到端审查更改。重点查看：
   - 用于切换模式的用户界面（UI）组件。
   - 用于保存用户偏好的本地存储。
   - 高对比度和浅色模式的层叠样式表（CSS）或样式更改。
   - 无障碍属性（无障碍富互联网应用程序（ARIA）标签、键盘导航等）。
   - 管理模式切换的 JavaScript/TypeScript 代码。
9. 返回 **Conversation** 选项卡。
10. 如果工作流正在等待批准，选择 **Approve and run workflows**。

    ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

11. 等待工作流完成。理想情况下，所有工作流都会通过。

> [!TIP]
> 想为无障碍改进再听取意见？在 PR 评论中提及 `@copilot`，并提出请求，例如“审查此 PR，找出其他 Web 内容无障碍指南（WCAG）相关问题”或“建议如何改进键盘导航”。Copilot 会启动新会话来处理这条评论。

## 可选练习 - 继续在本地探索

在集成开发环境（IDE）中与智能体迭代协作是一项需要反复练习的技能。你可以从 VS Code 开始以下后续探索：

- 在游戏详情页添加支持者意向表单。
- 在游戏列表页实现分页。
- 为 `src/lib/` 中的数据访问辅助函数添加输入验证和错误处理。
- 扩展无障碍智能体的工作范围，例如审查整个网站的键盘焦点顺序。

## 总结

恭喜，你已完成 VS Code 工作流！在本实验中，你：

- **使用 Playwright MCP 手动测试了功能。** 添加 Playwright MCP 服务器，让 Copilot 操作浏览器验证筛选功能，然后再创建拉取请求。
- **通过 agent mode 协调了跨技术栈的更改。** 在一个会话中添加了涉及客户端、服务器和测试的筛选功能。
- **使用了自定义智能体。** 从智能体选择器中选择专注于无障碍的自定义智能体，并观察它如何在存储库中实现高对比度模式。
- **管理并引导了智能体会话。** 在编辑器中审查建议的更改，接受需要的内容，并通过后续请求扩展会话，添加浅色模式。
- **通过拉取请求完成了整个流程。** 发布本地更改，并按照团队的方式端到端审查。

## 回顾和后续步骤

至此，VS Code 工作流中的必修部分已完成。工作坊已结束，你可以在此停止。

如果想进一步了解 Copilot 的智能体能力，其他工作流会通过不同界面介绍相关场景：

- 💻 **[命令行界面（CLI）工作流](../../cli/)** — 在终端中使用 Plan 和 Autopilot 模式、技能、自定义质量保证（QA）智能体、Playwright MCP、Agent Merge 和上下文感知交接，完成两项经过审查的更改。
- ☁️ **[云端智能体工作流](../../cloud/)** — 重点介绍将 issue 分配给云端智能体、通过 agents 页面监控会话，以及在拉取请求上异步迭代。

你也可以在已有成果上继续开发。[awesome-copilot][awesome-copilot]汇集了可按需改编的指令文件、自定义智能体和技能。

作为可选扩展，[可选：集成 Foundry][exercise-7]使用 VS Code 和 Microsoft Foundry Toolkit 准备模型、部署 Backer Concierge，并将其连接到网站。

## 资源

- [GitHub Copilot][github-copilot]
- [VS Code 中的 Copilot Chat][copilot-chat-vscode]
- [使用 agent mode][agent-mode]

---

| [← 上一课：监控和管理智能体][previous-lesson] |
|:--|

[previous-lesson]: ../5-managing-agents/
[exercise-4]: ../4-custom-agents/
[exercise-5]: ../5-managing-agents/
[exercise-7]: ../7-foundry-toolkit/
[github-copilot]: https://github.com/features/copilot
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
[awesome-copilot]: https://github.com/github/awesome-copilot
