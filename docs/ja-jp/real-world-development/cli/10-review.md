---
title: "レッスン 10 - 振り返りと次のステップ"
description: "Copilot CLI のワークフロー、2 つのプルリクエスト、再利用可能なカスタマイズ、追加リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

GitHub Copilot CLI を使い、Tailspin Toys の一連のワークフローに取り組みました。

- Codespace を準備し、Copilot CLI をインストールして、プロジェクトと登録済みの絞り込み Issue を確認しました。
- 星評価を追加し、転送されたブラウザーで確認して、最初のプルリクエスト (PR) を手動でマージしました。
- 絞り込み Issue から始め、Plan モードで方針を定義し、Autopilot モードで実装し、Interactive モードでレビューしました。
- カスタム指示でエージェントを導き、既存の `quality-checks` スキルをカスタマイズして、ユニットテスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーで絞り込みを確認しました。
- 品質保証 (QA) カスタムエージェントを作成して選び、要件、カバレッジ、スキルの結果、ブラウザーでの検証結果を評価しました。
- 絞り込み機能全体をレビューし、Agent Merge を許可して機能 PR を処理しました。
- コンテキスト、モデル、共有、cloud agent への任意の委任に使うスラッシュコマンドを確認しました。

## 作成したもの

ワークショップでは、それぞれ更新済みの `main` から作成する 2 つの PR を行います。

1. **星評価:** 既存の `starRating` と未評価状態をゲームカードに表示します。
2. **絞り込みと品質ワークフロー:** 絞り込み機能を実装し、指示を更新して機能に適用し、`quality-checks` のレポートをカスタマイズし、QA プロファイルと関連テストを追加します。

絞り込みの計画から PR の作成までは、同じ会話とブランチを使用しました。手順を簡潔にするため、作業を 1 つの PR にまとめました。

## さまざまな検証方法

自動テスト、自分で行うブラウザー確認、MCP 経由で Copilot が行うブラウザー確認を組み合わせました。`quality-checks` スキルではユニットテスト、lint、型チェックを実行し、追加した形式で結果を報告しました。QA では、PR の前にそれらの結果と要件、テストカバレッジのレビューをまとめました。

追加するテストは実際の不足を解決する必要があります。QA の実行で新しいテストが不要と判断される場合もあります。マージを許可する前にコードと証拠を確認し、変更後は影響を受ける検証結果を更新してください。

## ベスト プラクティス

Copilot に与えるコンテキストとツールは、その作業に影響します。このワークショップでは、指示を更新し、スキルをカスタマイズし、QA プロファイルを作成し、MCP サーバーを設定しました。こうしたカスタマイズは会話をまたいで再利用し、チームのニーズに合わせて調整できます。指示は標準を設定し、スキルは繰り返し実行するタスクを説明し、カスタムエージェントは専門的な役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果を確認してください。

タスクに合わせて**モードとモデル**を選びます。構築前に方針を検討するには **Plan**、対象を絞った変更に関与し続けるには **Interactive**、範囲が明確なタスクには **Autopilot** を使います。定型的な編集には高速なモデル、複雑な作業にはより高性能なモデルを選びます。

インフラストラクチャと同じように、コンテキストも重要です。何を、なぜ、どのように構築するのかを明確に伝えると、出力が大きく変わります。

## さらに確認する

主要なワークフローを終えました。Copilot CLI の追加機能として、次のコマンドも確認できます。

- `/review` はコードレビューエージェントに変更の分析を依頼します。
- `/rubber-duck` は問題を説明し、別の視点を得るために使います。
- `/fleet` は独立したサブタスクを並行して調整します。
- `/worktree` は別のタスクを分離します。
- `/delegate` はタスクを Copilot cloud agent に送ります。

## 次のステップ

ツールの習熟には、使い続けることが一番です。本番コード、趣味のコード、作りたいと思いながら手を付けていなかったアプリなどで活用してください。チームと学びを共有し、互いの経験から学びましょう。ドキュメントも引き続き確認してください。

ターミナルから Tailspin Toys を拡張する場合は、オプションの [Foundry Backer Concierge シリーズ][foundry]に進みます。別の環境も確認する場合は、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、または [Copilot cloud agent ワークショップ][cloud]を参照してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
- [Copilot CLI でプルリクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
