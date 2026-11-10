---
title: "レッスン 7 - 品質保証 (QA) エージェントの作成と使用"
description: "要件、quality-checks スキル、Playwright MCP を組み合わせる QA カスタムエージェントを作成します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

`quality-checks` スキルで自動チェックを実行し、Playwright MCP でブラウザーの絞り込み動作を確認しました。次は、明確な QA プロセスを持つカスタムエージェントにこれらの機能をまとめます。

このレッスンでは、次の操作を行います。

- カスタムエージェントが指示、スキル、MCP ツールと連携する方法を確認します。
- 再利用可能な品質保証プロファイルを作成して調べます。
- QA エージェントを選択し、絞り込み Issue に照らして結果をレビューします。

## シナリオ

Tailspin Toys では、プルリクエスト (PR) を作成する前に、要件、コード品質、自動チェック、テストカバレッジ、ブラウザー動作を一貫して確認したいと考えています。カスタムエージェントを使うと、QA プロセスを調整し、再利用可能なレポートを作成できます。

## カスタムエージェントとは

カスタムエージェントは、エージェントの目的、指示、使用可能なツールを記述した Markdown プロファイルで定義する Copilot の専門的な形態です。このワークショップでは `.github/agents/qa.agent.md` に QA の役割を定義し、Copilot CLI で選択します。

これまでに使ったカスタマイズには、それぞれ異なる役割があります。リポジトリの指示はチーム標準を説明し、`quality-checks` スキルは繰り返し実行できるチェックをまとめ、Playwright MCP はブラウザーツールを提供します。QA プロファイルは、それらを使って要件を評価し、結果を報告するよう Copilot に指示します。これらを置き換えるものではなく、別の会話も必要ありません。

## QA プロファイルを作成する

機能 PR を開く前に、実施するチェックと守るべき範囲を定めた再利用可能な QA プロファイルを作成します。

1. Codespace に戻り、絞り込みの会話が Interactive モードであることを確認します。
2. 既定のエージェントに、次のプロファイルの作成を依頼します。

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## プロファイルを確認する

QA エージェントを使う前に、意図したワークフローと制約が含まれていることを確認します。

1. `/diff` を入力し、`.github/agents/qa.agent.md` を開きます。
2. frontmatter を読みます。`description` は必須で、`name` は任意ですが、表示名として含めると分かりやすくなります。
3. プロファイルの指示を読み、要件を確認し、リポジトリの指示に従い、`quality-checks` スキルを実行し、Playwright MCP を使うことを確認します。
4. QA が根拠を示して報告し、実装コードを変更する前に確認を求め、変更をコミットしたり PR を開いたりしないことを確認します。
5. 責任や制約が不足している場合は、続行する前に既定のエージェントにプロファイルの修正を依頼します。

## Issue に対して QA を実行する

Copilot CLI は会話開始時にプロジェクトのエージェントを読み込みます。プロファイル作成後に同じ絞り込みの会話を再開し、QA を選ぶと、Issue と計画時の決定を引き継げます。

1. 次のコマンドを入力してエージェントを選択します。

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 作成直後は使用可能なエージェント一覧に表示されない場合がありますが、上記コマンドで有効にできます。

2. 次のプロンプトで、機能をレビューするよう QA エージェントに依頼します。

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA エージェントが作業を進める様子を確認します。
4. 完了したら、レポートを読みます。

## まとめと次のステップ

再利用可能な専門的役割を追加し、その作業をレビューしました。このレッスンでは、次の操作を行いました。

- カスタムエージェントが指示、スキル、MCP ツールと連携する方法を確認しました。
- 再利用可能な品質保証プロファイルを作成して確認しました。
- QA エージェントを選び、絞り込み Issue に対する結果をレビューしました。

実装、スキルの更新、QA プロファイル、テスト、検証レポートがそろいました。次は[それらを機能 PR にまとめ、Agent Merge を使用します][next-lesson]。

## リソース

- [Copilot CLI 用のカスタムエージェントを作成する][create-agents]
- [カスタムエージェントの構成][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
