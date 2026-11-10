---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

多くの組織では、未解決のセキュリティ問題、更新が必要なレガシー コード、バックログに残った機能要望など、技術的負債に直面しています。GitHub Copilot cloud agent は、コードの更新や機能の追加などを自律的に実行できます。作業が終わると、人間の開発者がレビューできるドラフトのプルリクエスト (PR) を作成します。時間のかかるタスクを任せることで、開発者はより大きな課題に集中できます。

この演習では、Copilot cloud agent を使って次のことを行います。

- コード生成環境をカスタマイズします。
- 操作を安全に行う方法を確認します。
- 範囲を明確に定めた Issue の重要性を学びます。
- Issue を Copilot に割り当てます。

## シナリオ

Tailspin Toys では、アプリケーションのエクスポート関数に TSDoc のドキュメント コメントがありません。まず、すべてのエクスポート関数にコメントを追加します。

デザイン チームはゲームを見つけやすくしたいと考えています。各ゲームの詳細ページに同じカテゴリの別のゲームを表示し、UX の受け入れテストに使える簡単な実装を希望しています。この作業は現在ブロッカーですが、より優先度の高い Issue があります。

このような作業は優先順位が下がりやすいため、Copilot cloud agent に割り当てるのに適しています。非同期で処理している間に別の作業を進め、後で結果をレビューできます。

## GitHub Copilot cloud agent について

[GitHub Copilot cloud agent][cloud-agent] は、人間の開発者と同様にバックグラウンドでタスクを実行できます。たとえば [GitHub Issue を Copilot に割り当てる][assign-issue]と、Copilot は進捗を追跡するドラフト PR を作成し、環境をセットアップしてタスクに取り組みます。作業中または完了後にセッションを確認できます。提案された解決策のレビュー準備ができると、プルリクエストで通知されます。

## 範囲が明確な指示の重要性

GitHub Copilot を使っても、考える作業を省略できるわけではありません。一見簡単な操作にも複雑さが潜んでいます。[cloud agent に依頼するタスクの範囲を明確に定めてください][cloud-agent-best-practices]。AI ペア プログラマーとして扱い、段階を踏んで学び、試し、調整します。生成 AI を導入しても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム指示

前の演習では、カスタム指示が Copilot を導く方法を確認しました。まだ `.github/copilot-instructions.md` を見ていない場合は、cloud agent に作業を割り当てる前に、結果への影響を確認できるよう読み取り専用で確認します。

GitHub Web UI または起動済みの Codespace で、次のファイルを開きます。

- `.github/copilot-instructions.md`: **Code standards** セクションの TypeScript 規約と TSDoc コメントの要件を確認します。
- `.github/instructions/unit-tests.instructions.md`: `applyTo` frontmatter が `**/*.test.ts` に指示を適用することを確認します。

次のセクションで `Code lacks documentation` Issue を cloud agent に割り当てると、これらの指示に由来する TSDoc、TypeScript 規約、ファイルヘッダーが PR に反映されます。後の演習で PR をレビューするときにも確認します。

## Copilot cloud agent の開発環境を設定する

コードを作るには環境の準備が必要です。タスクを Copilot に割り当てる場合も同様です。cloud agent は GitHub Actions の環境を使います。`.github/workflows/copilot-setup-steps.yml` に専用のセットアップ ワークフローを用意すると、作業前に必要な開発ツールや依存関係を設定できます。このテンプレートでは、Node.js、プロジェクトの依存関係、エンドツーエンドテスト用ブラウザー、単一 Astro アプリ用にマイグレーションとシードを行った SQLite データベースを利用できるよう、あらかじめ設定されています。

```yaml
name: "Copilot Setup Steps"

# リポジトリの "Actions" タブからセットアップ手順をテストできます。
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 必要最小限の権限を設定します。Copilot は操作用の独自トークンを受け取ります。
    permissions:
      # セットアップでリポジトリをクローンする場合 (依存関係のインストールなど) は contents: read が必要です。クローンしない場合は、手順の完了後に Copilot が自動でクローンします。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / アプリのセットアップ。アプリは Astro + Drizzle/libSQL です。
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # 単一 Astro アプリのビルドとテスト用に、ローカル SQLite データベースをマイグレーションしてシードします。
      - name: Set up the database
        run: npm run db:setup
```

通常の GitHub Actions ワークフローと同様ですが、次の点を確認してください。

- `copilot-setup-steps` という 1 つのジョブがあり、Copilot が PR 作業を開始する前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーがあるため、Copilot の実行を待たずにリポジトリの **Actions** タブから手動でテストできます。

## ドキュメントを追加する

ドキュメントは重要ですが、古くなっていたり不足していたりするプロジェクトもあります。Copilot cloud agent にドキュメント作成を依頼し、作業をバックグラウンドで進めてもらいます。後の演習で結果をレビューします。

1. 新しいブラウザー タブで github.com のリポジトリを開きます。
2. **Issues** タブを選びます。
3. **New issue** を選択して、新しい Issue のダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次を入力します。

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. **Create** を選択して Issue を作成します。
8. 右側の **Assign to Copilot** を選択して割り当てダイアログを開きます。

   ![Copilot を Issue に割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。
10. **Pull Requests** タブを選びます。
11. 新しく作成された PR を開きます。タイトルは `[WIP]: Code lacks documentation` などになります。PR が一覧にない場合は、少し待ってからブラウザーを更新します。
12. 数分後、Copilot の TODO リストが表示されたことを確認します。

> [!NOTE]
> TODO リストが PR に表示されるまで数分かかる場合があります。Copilot は環境を準備し、前述のワークフローを実行して、プロジェクトを分析し、問題への取り組み方を決めています。

13. TODO リストと実行予定のタスクを確認します。
14. PR のタイムラインを下にスクロールし、Copilot が Issue に取り組み始めたことを確認します。
15. **View session** ボタンを選択します。

   ![Copilot セッションを表示するボタン](../../../_images/ex4-view-session.png)

16. ライブ セッションをスクロールして、Copilot がコードと状態を調べ、計画を決め、コードを作成する様子を確認します。

数分かかる場合があります。cloud agent の利点は非同期で作業を任せ、別のタスクに集中できることです。もう 1 つのタスクを割り当てたら、アプリの機能開発に取り組みます。

## ゲーム詳細ページに関連ゲームを追加する

cloud agent に作業を分けて任せれば、自分は別のタスクに取り組めます。デザイン チーム向けの関連ゲーム欄も cloud agent に依頼します。

1. github.com のリポジトリに戻ります。
2. **Issues** タブ、続いて **New issue** を選択します。
3. **Blank issue** を選択します。
4. **Title** に `Show related games on the game details page` と入力します。
5. **Description** に次の内容を入力します。

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

6. **Create** を選択します。
7. 右側の **Assign to Copilot** を選び、ダイアログで **Assign** を選択します。

   ![Copilot を Issue に割り当てる画面](../../../_images/shared-assign-copilot.png)

Issue の最初のコメントに 👀 が表示され、Copilot が作業中であることが分かります。

Copilot は 2 つ目の依頼にも取り組み始めました。ソフトウェア エンジニアのように作業するため、完了まで常に監視する必要はありません。後で結果をレビューします。次はカスタムエージェントの作成と使用を確認します。

## まとめと次のステップ

[GitHub Copilot cloud agent][copilot-agents] に Issue を割り当て、非同期で作業させる方法を学びました。技術的負債の解消、新機能の作成、フレームワーク間のコード移行などに利用できます。

- コード生成環境をカスタマイズしました。
- 操作を安全に行う方法を確認しました。
- 範囲を明確に定めた Issue の重要性を学びました。
- Issue を Copilot に割り当てました。

cloud agent がバックグラウンドで作業する間、次はカスタムエージェントの作成と使用に進みます。[Copilot cloud agent は Model Context Protocol (MCP) サーバー][cloud-agent-mcp]と、前の演習で扱ったカスタム指示も利用できます。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローのベスト プラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタムエージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
