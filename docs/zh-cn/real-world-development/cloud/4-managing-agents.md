---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前几项练习中，你让 Copilot 云智能体处理了三项旨在改善用户体验和添加功能的任务。云智能体虽然可以异步自主工作，但监控这些任务仍然很重要。

你可以使用多种工具管理分配给云智能体的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个代理控制台中，你可以查看所有有开放拉取请求 (PR) 的智能体任务，检查已执行的操作，也可以引导正在进行的会话。

本课将介绍如何：

- 查看智能体页面，监控云智能体任务。
- 引导正在进行的会话，请求添加其他功能。

## 场景

将高对比度模式任务分配给智能体后，团队意识到也可以添加浅色模式。由于网站样式和切换功能正在更新，加入这项功能很合适。现在引导智能体，要求它同时添加浅色模式和高对比度模式。

## 查看 Copilot 云智能体任务

先查看分配给 Copilot 云智能体的任务状态。

1. 打开 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主面板和左侧面板中的任务列表。列表应包含已分配给 Copilot 的任务，例如：
    - 更新代码文档。
    - 生成用于修改游戏的应用程序编程接口 (API)。
    - 为网站添加高对比度模式。
3. 选择一项正在运行的任务，查看 Copilot 已执行的操作，例如：
    - 从存储库检出代码。
    - 创建 Copilot 的工作环境。
    - 设置模型上下文协议 (MCP) 服务器。
    - 执行完成任务所需的其他步骤。

> [!NOTE]
> 具体步骤会根据 Copilot 的工作状态和所采用的方法而变化。

4. 同时查看右侧显示的 PR 面板，以便监控 PR 和已更改文件。

## 引导云智能体

查看当前任务后，在 Copilot 处理高对比度模式期间，请求它同时添加浅色模式切换开关。

1. 选择与添加高对比度模式相关的会话。会话标题会因 Copilot 采用的名称和当前工作状态而异。

    ![代理控制台中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，直到它完成环境设置并开始处理任务。看到类似的消息时，就表示已开始工作。
3. 在 **Steer active session while Copilot is working** 对话框中输入以下提示：

    ```plaintext
    添加高对比度模式时，也请添加浅色模式。用户也应能通过一个开关选择所需的显示模式。
    ```

    ![智能体页面中的云智能体任务，突出显示 Steer active session while Copilot is working 对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示。
5. 确认 Copilot 已收到提示，并将其纳入工作流程。

## 让 Copilot 继续工作

和之前一样，Copilot 会继续处理更新后的任务。在完成你发送提示时正在执行的步骤后，它会把新要求纳入工作流程。

这同样需要几分钟。等待期间，可以回顾目前学到和探索的内容。

## 总结与后续步骤

本课介绍了 Copilot 智能体页面，这里是监控和引导 GitHub Copilot 云智能体任务的中心位置。你可以跟踪所有正在进行和已完成的任务、审查工作，并重定向正在运行的任务以调整范围或提供额外指导。

本课中，你：

- 使用代理控制台和智能体页面监控了云智能体任务。
- 重定向了正在进行的会话，请求添加其他功能。

Copilot 正在完成无障碍功能。接下来，[迭代 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
