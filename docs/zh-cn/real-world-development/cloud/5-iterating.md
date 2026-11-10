---
title: "练习 5：迭代改进 GitHub Copilot 的工作成果"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

## 审查工作成果

在本实验中，你使用 GitHub Copilot 完成了多个旨在改善用户体验和添加功能的任务：为代码添加文档、实现供设计团队迭代的相关游戏功能，以及实现包括高对比度和浅色模式切换在内的无障碍功能。现在查看代码更改，必要时向 Copilot 提供反馈，进一步完善成果。

### 场景

如前所述，加入生成式人工智能 (AI) 并不会改变软件设计和开发运维 (DevOps) 的基本原则。我们始终需要审查生成的代码，并遵循常规的 DevOps 流程。接下来，在为团队其他成员启用审查前，先查看 GitHub Copilot 对文档、相关游戏功能和无障碍功能的建议。

## GitHub Copilot 云智能体的安全性

Copilot 云智能体会异步且自主地执行任务，因此设有安全限制，确保操作安全：

- Copilot 对存储库只有读取权限，对写入操作的权限**仅限于**用于提交代码的分支。
- 云智能体在 GitHub Actions 中运行，并在独立的临时环境中工作。
- 运行任何 GitHub Actions 工作流前，都需要人工批准。
- 默认情况下，[对外部资源的访问受到限制](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)，包括模型上下文协议 (MCP) 服务器。

## 审查生成的文档

先查看 GitHub Copilot 云智能体创建的第一个拉取请求 (PR)，其中包含为代码添加的文档。你将使用 GitHub.com 上的标准 PR 界面进行审查。

> [!NOTE]
> 查看 PR 时，可能会看到 GitHub Copilot 被防火墙阻止的警告。这是**预期行为**，因为 Copilot 默认只能有限地访问外部资源，包括外部 MCP 服务器。如果需要，可以[自定义或禁用 Copilot 云智能体防火墙][agent-firewall]。

1. 返回 github.com 上的存储库。
2. 选择 **Pull Requests**，打开 PR 列表。
3. 打开标题类似 **Add missing documentation** 的 PR。标题也可能更具体。

> [!NOTE]
> 如果 Copilot 仍在处理任务，PR 标题会带有 **[WIP]** 标记。请等待 Copilot 完成。这可能需要几分钟，可以趁此休息或回顾已学内容。

4. PR 准备就绪后，选择 **Files changed** 选项卡并审查更改。

    ![Files changed 选项卡](../../../_images/shared-pr-files-changed.png)

5. 查看更新后的代码，其中包含新生成的 TSDoc 文档注释及其他文档。具体更改会有所不同。

    查看更改时，留意 TSDoc 文档注释、TypeScript 规范和文件注释头。这些内容来自你在练习 2 开始时查看的自定义指令文件。

6. 确认更改符合预期后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有等待批准的工作流提示。
8. 如果有工作流等待批准，选择 **Approve and run workflows**。

   ![Approve and run workflows 按钮](../../../_images/shared-approve-workflows.png)
9. 工作流应会进入 PR 的检查队列。如果一切正常，单体 Astro 应用的项目检查将通过。此过程可能需要几分钟。

## 请求 GitHub Copilot 修改

与 Copilot 协作并非单向过程。你可以像对待团队成员一样，在 PR 评论或代码行内评论中提及 Copilot。Copilot 会读取评论并启动新会话来处理请求。由于结果并非完全确定，无法提供必须照搬的请求文本。可以要求 Copilot：

- 在每个代码文件顶部添加简短的文件注释头，说明文件用途。
- 为 TypeScript 和 Astro 文件添加 TSDoc 文档注释。
- 创建 README，介绍 Astro 应用的结构。

1. 添加评论，请求修改生成的文档，并像提及用户一样标记 **@copilot**。可以使用上面的建议，也可以提出其他希望添加到代码库文档中的内容。
2. 选择 **View Session**，查看 Copilot 执行修改的过程。Copilot 会启动新会话来应用更改。
3. 选择 **Back to pull request** 可返回 PR。

    ![Back to pull request 按钮](../../../_images/ex7-back-to-pr.png)

4. Copilot 完成修改后，PR 中应出现新的提交。
5. 选择 **Files changed** 选项卡，审查更改。

可以继续迭代，直到满意为止。满意后，将 PR 从草稿状态改为准备审查，然后合并到主分支。

![将 PR 从草稿状态改为准备审查](../../../_images/ex7-ready-for-review.png)

## 审查相关游戏功能

接下来查看 Copilot 为解决游戏详情页显示相关游戏议题而创建的 PR。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Show related games on the game details page** 的 PR。标题也可能更具体。
4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 确认更改符合预期后，返回 **Conversation** 选项卡并向下滚动。
6. 查看是否有等待批准的工作流提示。
7. 如果有工作流等待批准，选择 **Approve and run workflows**。

   ![Approve and run workflows 按钮](../../../_images/shared-approve-workflows.png)
8. 工作流应会进入 PR 的检查队列。如果一切正常，单体 Astro 应用的项目检查将通过。此过程可能需要几分钟。
9. **可选：**可以在 Codespace 中切换到该分支，手动测试相关游戏功能。打开 Codespace 终端并运行以下命令，将 `<branch-name>` 替换为 Copilot 创建的分支名称，例如 **copilot/fix-8**：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot 已实现相关游戏功能。和之前一样，可以继续迭代并请求云智能体修改。例如，可以调整显示的相关游戏数量，或要求添加文件注释头和 TSDoc 文档注释（请记住，这项工作是在更新自定义指令**之前**分配的）。和之前一样，在 **Conversation** 选项卡中添加评论，Copilot 会读取评论并启动新会话。

## 审查无障碍功能

最后，审查通过无障碍自定义智能体实现的功能。此 PR 应包含练习 3 中分配的高对比度模式，以及练习 4 中在代理控制台请求的浅色模式。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Add high contrast mode to website** 的 PR。标题也可能更具体。

> [!NOTE]
> 如果 Copilot 仍在处理任务，PR 标题会带有 **[WIP]** 标记。请等待 Copilot 完成，这可能需要几分钟。

4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 审查实现，重点检查：
   - 用于切换模式的开关用户界面组件。
   - 用于保存用户偏好的本地存储。
   - 高对比度和浅色模式的层叠样式表 (CSS) 或样式更改。
   - 无障碍属性，如无障碍富互联网应用程序 (ARIA) 标签和键盘导航。
   - 管理模式切换的 JavaScript/TypeScript 代码。

6. 确认更改符合预期后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有等待批准的工作流提示。
8. 如果有工作流等待批准，选择 **Approve and run workflows**。

   ![Approve and run workflows 按钮](../../../_images/shared-approve-workflows.png)
9. 工作流应会进入 PR 的检查队列。如果一切正常，单体 Astro 应用的项目检查将通过。此过程可能需要几分钟。
10. **可选：**可以在 Codespace 中切换到该分支，手动测试无障碍功能。打开 Codespace 终端并运行以下命令，将 `<branch-name>` 替换为 Copilot 创建的分支名称：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    然后启动应用，在浏览器中测试高对比度和浅色模式切换，并确认设置能在重新加载页面后保留。

无障碍自定义智能体帮助 Copilot 按照无障碍最佳实践实现功能。如果发现无障碍问题或改进点，可以像处理之前的 PR 一样，在评论中标记 **@copilot** 请求修改。

## 可选练习 — 继续委派任务

云智能体适合处理待办事项，让你能转而处理其他工作。可以在自己的存储库中创建更多议题并分配给 Copilot，练习这种工作方式。例如：

- 在游戏详情页创建支持者意向表单。
- 为游戏列表页添加分页。
- 为数据访问辅助函数添加输入验证和错误处理。

## 总结

你已完成云智能体工作环境的练习。在这些课程中，你：

- **检查了存储库提供的自定义指令文件**，以便之后观察它们对云智能体输出的影响。
- **将议题分配给 Copilot 云智能体**，并观察它设置环境、制定计划和异步执行任务。
- **创建并使用自定义智能体**处理无障碍工作，添加高对比度和浅色模式切换。
- **使用 Copilot 智能体页面作为代理控制台**，监控并引导无障碍会话。
- **审查并迭代云智能体创建的拉取请求**，通过标记 `@copilot` 请求修改并批准工作流。

## 回顾与后续步骤

云智能体工作环境的练习已完成。其他工作环境可以帮助你继续探索：

- 🖥️ **[VS Code 工作环境](../../vscode/)** — 在集成开发环境 (IDE) 中体验 Copilot Chat 智能体模式和 MCP 集成。
- 💻 **[CLI 工作环境](../../cli/)** — 在终端中交付两项经过审查的更改，体验 Plan 和 Autopilot 模式、智能体技能、自定义质量保证 (QA) 智能体、Playwright MCP、Agent Merge，以及可选的 `/delegate` 云智能体桥接。

还可以在自己的存储库中尝试以下后续练习：

- 将重构或测试覆盖率议题分配给云智能体。
- 为其他领域创建自定义智能体。
- 为其他技术栈设置 `copilot-setup-steps.yml`。

## 资源

- [GitHub Copilot][github-copilot]
- [关于 Copilot 智能体][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]
- [配置 Copilot 云智能体防火墙][agent-firewall]

---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
[previous-lesson]: ../4-managing-agents/
