---
title: "练习 4 - 自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

GitHub Copilot 中的[自定义智能体][custom-agents-concept]是针对开发工作流中特定任务或领域定制的人工智能 (AI) 助手。你可以在存储库的 `.github/agents` 文件夹中创建 Markdown 文件来定义智能体，提供有针对性的指令、最佳实践、编码模式和领域知识，帮助 Copilot 更有效地完成特定类型的工作。团队可以将专业经验整理成可复用的智能体，例如确保符合[《Web 内容无障碍指南》 (WCAG)][wcag]的无障碍智能体、遵循安全编码实践的安全智能体，或维护一致测试模式的测试智能体。

自定义智能体由项目 `.github/agents` 文件夹中的 Markdown 文件定义，也可以在 `~/.copilot/agents` 中全局定义。每个文件都包含 YAML frontmatter，至少需要 `name` 和 `description` 字段；之后是 Markdown 提示，用于定义智能体的行为、专长和指令。

### 自定义智能体与智能体技能的区别

自定义智能体和[智能体技能][agent-skills-concept]有些相似：两者主要通过 Markdown 文件定义，都会告诉 AI 如何执行任务。最简单的区分方式是：**自定义智能体负责工作，技能提供工具。**

自定义智能体拥有自己的上下文窗口，并负责协调技能（甚至其他智能体）完成工作。本实验中的无障碍自定义智能体会根据无障碍指南审查并更新网站；它还可以调用拉取请求工作流技能或运行和管理测试的技能。

> [!NOTE]
> 编写自定义智能体没有唯一正确的方法。和其他 AI 功能一样，应在自己的环境和场景中测试并不断迭代。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## 场景

Tailspin Toys 致力于让所有用户都能使用其众筹平台，不受视力能力或偏好的影响。近期用户反馈指出，目前的深色主题对比度不足，部分用户难以阅读。为解决这一无障碍问题，设计团队要求实现可由用户开启或关闭的高对比度模式。

无障碍功能至关重要，因此希望尽快实现。你将使用自定义智能体生成该功能。

本练习将介绍如何：

- 查看现有的无障碍自定义智能体。
- 在 Copilot Chat 中使用无障碍智能体实现高对比度模式。

## 查看无障碍自定义智能体

项目已为无障碍工作创建了自定义智能体。先查看其内容，了解它将如何引导 Copilot。

返回 Codespace，在终端中从 `main` 创建新分支，用于无障碍功能工作。这样可以让筛选功能 PR（练习 3）保持独立：

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. 打开 `.github/agents/accessibility.md`。
2. 查看包含 `name` 和 `description` 字段的 YAML frontmatter。

> [!CAUTION]
> 自定义智能体必须包含 `name` 和 `description` frontmatter 字段。

3. 继续阅读后续部分，了解其中介绍的内容：
   - 为无障碍网站生成代码时的核心职责。
   - 无障碍最佳实践。
   - 超文本标记语言 (HTML)、层叠样式表 (CSS) 和 JavaScript 示例。
   - 常见陷阱和错误。

## 在 Copilot Chat 中使用自定义智能体

VS Code 会在 Copilot Chat 视图底部的智能体下拉列表中显示 `.github/agents` 内定义的所有自定义智能体。选择自定义智能体后，该聊天会话会遵循相应的指令和工具配置。

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。不同练习所用的模式和模型可能不同；相关步骤会在需要时说明。

1. 如果 Chat 视图的智能体下拉列表中尚未选择 **Agent**，请先选择它。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

2. 选择 Chat 视图底部的智能体下拉列表。它会显示当前使用的智能体；默认是 **default**。
3. 从可用智能体列表中选择 **Accessibility agent**。
4. 向无障碍智能体发送以下提示：

    ```plaintext
    为网站添加高对比度模式。提供一个用户可以操作的高对比度切换开关，并使用浏览器本地存储设置，让偏好在重新加载页面后仍然保留。
    ```

5. Copilot Chat 会开始工作：探索代码库、提出更改并编辑项目文件。每项编辑都会以内联方式显示在聊天中，并包含文件路径和供你审查的差异。
6. 随着编辑应用到项目，**Files changed** 指示器会更新，显示智能体已修改的文件。

> [!NOTE]
> 此过程可能需要几分钟。Copilot 正在实际修改存储库中的文件；工作时可能会编辑 Astro 组件、CSS 和相关测试等现有文件。

下一练习将介绍如何查看并引导这项正在进行的工作。

## 总结与后续步骤

本课介绍了 GitHub Copilot 中的[自定义智能体][custom-agents]，也就是针对特定任务和领域定制的 AI 助手。自定义智能体可以将团队经验和标准整理成可复用的配置，引导 Copilot 更有效地完成特定类型的工作。

本课中，你：

- 了解了如何定义自定义智能体。
- 在 Copilot Chat 智能体模式中使用了自定义智能体。

接下来，[监控并引导智能体的工作][next-lesson]，在更改生成时进行审查，并在同一会话中添加浅色模式切换开关。

## 资源

- [关于自定义智能体][custom-agents]
- [在 IDE 中创建自定义智能体][creating-custom-agents-ide]
- [VS Code 中的自定义智能体][custom-agents-vscode]
- [自定义智能体配置][custom-agents-config]
- [Awesome Copilot 上的自定义智能体][awesome-copilot-agents]

---

| [← 上一课：使用 Playwright MCP 服务器测试功能][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
