---
title: "演習 3 - カスタムエージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタムエージェントとは

GitHub Copilot の[カスタムエージェント][custom-agents-concept]を使うと、開発ワークフローの特定のタスクや分野に合わせた人工知能 (AI) アシスタントを作成できます。リポジトリの `.github/agents` フォルダー内に Markdown ファイルを作り、専門的な指示、ベスト プラクティス、コーディング パターン、分野固有の知識を与えることで、特定の作業を効果的に行えるようにします。たとえば、[Web Content Accessibility Guidelines (WCAG)][wcag] 準拠を確認するアクセシビリティ エージェント、安全なコーディングを確認するセキュリティ エージェント、一貫したテスト パターンを守るテスト エージェントを作成できます。

カスタムエージェントは、プロジェクト内の `.github/agents` またはグローバルな `~/.copilot/agents` にある Markdown ファイルで定義します。各ファイルには少なくとも `name` と `description` を含む YAML frontmatter を記述し、その後に動作、専門知識、指示を定義する Markdown プロンプトを続けます。

### カスタムエージェントとエージェント スキルの違い

カスタムエージェントと[エージェント スキル][agent-skills-concept]には重なる部分があります。どちらも主に Markdown ファイルで定義し、AI に作業の方法を伝えます。分かりやすく言うと、**カスタムエージェントは作業者、スキルはツール**です。

カスタムエージェントには独自のコンテキスト ウィンドウがあり、作業の一部としてスキルやほかのエージェントを調整できます。この演習では、アクセシビリティ エージェントがサイトをガイドラインに照らして確認・更新します。その際、プルリクエスト作成ワークフローやテスト実行を管理するスキルを呼び出すこともできます。

> [!NOTE]
> カスタムエージェントの作成に唯一の正解はありません。AI のほかの活用方法と同じように、環境やシナリオに合わせて試し、改善してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

この演習では、カスタムエージェントについて次のことを学びます。

- カスタムエージェントの定義方法
- タスクをカスタムエージェントに割り当てる方法

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず、すべてのユーザーがクラウドファンディング プラットフォームを利用できるようにしたいと考えています。最近、現在のダークテーマはテキストと背景色のコントラストが不十分で、読みにくいという意見が寄せられました。デザイン チームは、ユーザーが切り替えられるハイコントラスト モードを求めています。

アクセシビリティは重要なため、カスタムエージェントを利用して機能をすばやく作成します。

## アクセシビリティ カスタムエージェントを確認する

アクセシビリティ用のカスタムエージェントがすでに用意されています。Copilot を導く内容を確認します。

1. Codespace に戻り、`.github/agents/accessibility.md` を開きます。
2. `name` と `description` を含む YAML frontmatter を確認します。

> [!CAUTION]
> カスタムエージェントには `name` と `description` を含む frontmatter が必要です。

3. 続くセクションを確認します。
   - アクセシブルなサイト用のコードを生成するときの主な責任
   - アクセシビリティのベスト プラクティス
   - HTML、CSS、JavaScript のコード例
   - よくある問題と間違い

## Issue を作成して割り当てる

Mission control は、環境内のエージェントを操作する場所です。Copilot cloud agent にタスクを割り当て、監視し、追加のガイダンスを与えられます。ここではハイコントラスト モードの作成を依頼します。

1. リポジトリに移動します。
2. **Issues** タブを選びます。
3. **New issue**、続いて **Blank issue** を選択します。
4. **Title** に `Add high contrast mode to website` と入力します。
5. **Description** に次を入力します。

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

6. **Create** を選択します。
7. 右側の **Assign to Copilot** を選択します。
8. 一覧から **Accessibility agent** を選びます。

   ![Cloud agent の割り当て画面で、カスタムエージェントと Accessibility が選択されている](../../../_images/ex5-select-custom-agent.png)

9. **Assign** を選択します。
10. Copilot がバックグラウンドで作業を始めることを確認します。

## まとめと次のステップ

[カスタムエージェント][custom-agents]は、特定のタスクや分野に合わせた GitHub Copilot の専門的な AI アシスタントです。チームの知識や標準を再利用可能なエージェントに組み込み、Copilot の作業を導けます。

- カスタムエージェントの定義方法を学びました。
- タスクをカスタムエージェントに割り当てました。

Copilot がハイコントラスト モードを実装している間に、次は [Mission control からセッションを監視して方向付けます][next-lesson]。

## リソース

- [カスタムエージェントについて][custom-agents]
- [組織でカスタムエージェントを使う準備][org-custom-agents]
- [エンタープライズでカスタムエージェントを使う準備][enterprise-custom-agents]

---

| [← 前のレッスン: GitHub Copilot cloud agent][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
