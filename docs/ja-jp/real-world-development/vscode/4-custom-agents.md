---
title: "演習 4 - カスタムエージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタムエージェントとは

GitHub Copilot の[カスタムエージェント][custom-agents-concept]を使うと、開発ワークフローの特定のタスクや分野に特化した人工知能 (AI) アシスタントを作成できます。リポジトリの `.github/agents` フォルダーに Markdown ファイルを置き、対象を絞った指示、ベストプラクティス、コーディングパターン、分野固有の知識を定義すると、Copilot がその作業を効果的に進められます。チームの専門知識を再利用可能なエージェントとしてまとめることもできます。たとえば、[Web Content Accessibility Guidelines (WCAG)][wcag] への準拠を確認するアクセシビリティエージェント、安全なコーディングを支援するセキュリティエージェント、一貫したテストパターンを守るテストエージェントを作成できます。

カスタムエージェントは、プロジェクト内の `.github/agents` フォルダー、またはグローバルな `~/.copilot/agents` にある Markdown ファイルで定義します。各ファイルには、少なくとも `name` と `description` を含む YAML Ain't Markup Language (YAML) フロントマターと、エージェントの動作、専門知識、指示を記述する Markdown プロンプトが必要です。

### カスタムエージェントとエージェントスキルの違い

カスタムエージェントと[エージェントスキル][agent-skills-concept]には、役割が重なる部分があります。どちらも主に Markdown ファイルで定義し、AI に作業の進め方を伝えます。分かりやすく言うと、**カスタムエージェントは作業者、スキルはツール**です。

カスタムエージェントには独自のコンテキストウィンドウがあり、作業の一環としてスキルやほかのエージェントを編成できます。この演習のアクセシビリティ用カスタムエージェントは、サイトをアクセシビリティガイドラインに照らして確認し、更新します。その作業の中で、プルリクエストのワークフロースキルやテストを実行・管理するスキルを呼び出すこともできます。

> [!NOTE]
> カスタムエージェントの作成に唯一の正解はありません。AI を使うほかの作業と同じように、自分の環境やシナリオに合わせて試し、改善してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず、誰もがクラウドファンディングプラットフォームを利用できるようにしたいと考えています。最近、現在のダークテーマは文字と背景のコントラストが不十分で、読みにくいというフィードバックが寄せられました。そこでデザインチームは、オンとオフを切り替えられる高コントラストモードを求めています。

アクセシビリティは重要なため、カスタムエージェントを使って機能をすばやく実装します。

この演習では、次のことを行います。

- 既存のアクセシビリティ用カスタムエージェントを確認します。
- Copilot Chat でアクセシビリティエージェントを使い、高コントラストモードを実装します。

## アクセシビリティ用カスタムエージェントを確認する

あらかじめ用意されたエージェントが Copilot をどう導くのかを理解するため、内容を確認します。まず、codespace でアクセシビリティ作業用の新しいブランチを `main` から作成します。演習 3 のフィルター機能の PR とは分けて作業します。

1. codespace に戻り、ターミナルを開きます。
2. 次のコマンドを実行して、`main` からブランチを作成します。

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

3. `.github/agents/accessibility.md` を開きます。
4. `name` と `description` フィールドがある YAML フロントマターを確認します。

> [!CAUTION]
> `name` と `description` のフロントマターは、カスタムエージェントに必須です。

5. 続くセクションを読み、アクセシブルな Web サイトのコード生成に関する次の内容を確認します。
   - エージェントの主な役割。
   - アクセシビリティのベストプラクティス。
   - HyperText Markup Language (HTML)、Cascading Style Sheets (CSS)、JavaScript のコード例。
   - よくある問題と避けるべきミス。

## Copilot Chat でカスタムエージェントを使う

VS Code の Copilot Chat ビュー下部にあるエージェントのドロップダウンには、`.github/agents` で定義されたカスタムエージェントが表示されます。エージェントを選択すると、その指示とツールに合わせてチャットセッションを設定できます。

> [!TIP]
> **Copilot Chat を開く**
>
> 以下の演習を始める前に、codespace に戻り、Copilot Chat パネルを開いて **New Chat** を選択し、新しい会話を開始します。モードとモデルの選択は演習ごとに異なるため、必要な箇所で説明します。

1. Chat ビューのエージェントのドロップダウンで、**Agent** が選択されていない場合は選択します。

   ![Chat ビューのエージェント選択メニューを示すスクリーンショット。](../../../_images/shared-chat-mode-selector.png)

2. Chat ビュー下部のエージェントのドロップダウンを選択します。現在のエージェントが表示されます。既定では **default** です。
3. 使用可能なエージェントの一覧から **Accessibility agent** を選択します。
4. 次のプロンプトをアクセシビリティエージェントに送信します。

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

5. Copilot Chat がコードベースを調べ、変更を提案してプロジェクトのファイルに適用します。変更はファイルパスと差分とともにチャット内に表示されます。
6. 編集が適用されると、**Files changed** の表示にエージェントが変更したファイルが反映されます。

> [!NOTE]
> この作業には数分かかることがあります。Copilot はリポジトリ内のファイルを実際に変更します。Astro コンポーネント、CSS、関連するテストなどが対象になります。

進行中の作業のレビューと方向付けは、次の演習で行います。

## まとめと次のステップ

この演習では、次のことを行いました。

- 既存のアクセシビリティ用カスタムエージェントを確認しました。
- Copilot Chat でアクセシビリティエージェントを使い、高コントラストモードを実装しました。

次は[エージェントの作業を監視して方向付け][next-lesson]、変更を確認しながら、同じセッションにライトモードの切り替えを追加します。

## リソース

- [カスタムエージェントについて][custom-agents]
- [統合開発環境 (IDE) でカスタムエージェントを作成する][creating-custom-agents-ide]
- [VS Code のカスタムエージェント][custom-agents-vscode]
- [カスタムエージェントの構成][custom-agents-config]
- [awesome-copilot のカスタムエージェント][awesome-copilot-agents]

---

| [← 前のレッスン: Playwright MCP で機能をテストする][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
