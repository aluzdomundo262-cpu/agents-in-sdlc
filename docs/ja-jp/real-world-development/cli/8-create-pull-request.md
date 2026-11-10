---
title: "レッスン 8 - 機能プルリクエストの作成とマージ"
description: "絞り込み、指示、スキルの更新、品質保証 (QA) プロファイル、テストをまとめてレビューし、プルリクエスト (PR) を作成して Agent Merge を使用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

絞り込み機能、指示の更新、スキルの更新、品質保証 (QA) プロファイル、テストが、1 つのブランチに保存されています。まとめてレビューしてプルリクエストを開きましょう。星評価のプルリクエスト (PR) は手動でマージしましたが、今回は **Agent Merge** に処理を任せます。

> [!NOTE]
> 通常は機能、指示の更新、スキルの更新、QA エージェントを複数の PR に分けます。このワークショップでは手順を簡潔にするため、絞り込みと品質に関する一連の作業を 1 つの会話とブランチで進め、1 つの PR にまとめました。

このレッスンでは、次の操作を行います。

- Agent Merge と、マージまでのワークフローを自動化する方法を学びます。
- 機能全体の変更と検証結果を確認します。
- 絞り込み PR を作成します。
- レビュー後に Agent Merge を有効にし、PR がマージされたことを確認します。

## シナリオ

絞り込み機能の開発では、Copilot を使って機能を計画、実装、検証しました。Tailspin Toys では PR に関する残りの作業を自動化したいと考えていますが、マージの許可は開発者が管理します。

## Agent Merge について

**Agent Merge** は、プルリクエストをマージ可能にするために必要な残りの作業を自動化します。有効にすると、Copilot は継続的インテグレーション (CI) チェックの失敗を修正し、レビューコメントに対応し、必要に応じてリベースするなど、PR を妨げている問題に取り組みます。その後、リポジトリで許可されていれば GitHub の自動マージを有効にします。

これまでは **Merge pull request** を自分で選択していました。Agent Merge に任せる場合も、有効にする前に作業をレビューし、準備ができていることを確認してください。

## Agent Merge で PR を管理する

コードを作成したら、まとめてレビューして PR を作成し、残りの処理を Agent Merge に任せます。

1. Codespace に戻ります。
2. `/agent` を入力してエージェント ダイアログを開きます。
3. 選択肢から **Default** を選び、<kbd>Enter</kbd> を押します。
4. `/pr create` コマンドで新しい PR を作成します。
5. `/pr agentmerge` を実行して Agent Merge を有効にします。
6. Copilot が PR の継続的インテグレーションを監視します。すべて成功するとマージします。
7. Copilot が「PR #14 was squash-merged successfully.」などのメッセージを表示したことを確認します。

> [!IMPORTANT]
> Agent Merge は、必須の承認、ブランチ保護、マージキュー、リポジトリ設定、または不足している権限を回避しません。処理がブロックされた場合は、報告された理由を確認し、リポジトリで許可されている手順に従ってレビュー済みのマージを手動で完了します。

## まとめと次のステップ

コードの生成、テストと検証に加えて、プルリクエストの処理も自動化しました。このレッスンでは、次の操作を行いました。

- Agent Merge と、マージまでのワークフローを自動化する方法を学びました。
- 機能全体の変更と検証結果を確認しました。
- 絞り込み PR を作成しました。
- レビュー後に Agent Merge を有効にし、PR がマージされたことを確認しました。

次は[コンテキスト、モデル、共有、cloud agent への任意の委任に使える Copilot CLI のスラッシュコマンドを確認します][next-lesson]。

## リソース

- [Copilot CLI でプルリクエストを管理する][manage-prs]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
