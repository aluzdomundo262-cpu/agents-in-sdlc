---
title: "レッスン 3 - エージェントモード: Plan と Autopilot"
description: "Plan で方針を合意し、Autopilot で Issue に基づく絞り込み機能を実装して、Interactive モードで結果をレビューします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

最初に小さな機能を追加しました。より大きな変更には、さらに確実なプロセスが必要です。GitHub Copilot CLI は組織の既存の開発フローに沿って作業できます。このレッスンから数回にわたり、Issue を起点に機能を作成し、コードの妥当性と機能の動作を確認して、プロジェクトにマージするまでの一般的なエージェント開発プロセスを進めます。

> [!NOTE]
> 機能開発の間は、同じ会話とブランチを使います。通常はファイルの種類ごとにブランチや PR を分けますが、ここでは主な概念に集中できるように簡略化します。

このレッスンでは、次の操作を行います。

- GitHub Issue から Copilot の会話を開始します。
- Plan モードで要件を定義します。
- Autopilot モードで機能を実装します。
- コードをレビューします。
- 転送されたブラウザーで機能を手動で検証します。

この後、リポジトリの指示を更新し、既存の `quality-checks` スキルをカスタマイズして、MCP による検証を追加し、QA エージェントを作成して機能 PR を開きます。

## シナリオ

Tailspin Toys のカタログが増えているため、訪問者がカテゴリとパブリッシャーでゲームを絞り込めるようにします。バックログの Issue には機能が記載されていますが、カテゴリを組み合わせる方法など、実装前に合意すべき詳細があります。Plan モードで方針を決めてから、Autopilot に範囲を明確にした実装を任せます。

## 背景

AI コーディングエージェントを開発に取り入れても、基本的な工程は変わりません。一般的な流れは次のとおりです。

1. 必要な作業を説明する Issue から始めます。
2. 実装する内容を計画します。
3. コードを作成してレビューします。
4. テストを実行してコードを検証します。
5. 新しい機能を手動で検証します。
6. プルリクエスト (PR) を作成します。
7. コードレビューと継続的インテグレーションが成功したら、コードをマージします。

> [!NOTE]
> チームや組織によって具体的な手順は異なりますが、多くの場合は上記の流れを調整したものになります。

この標準的な進め方に従うと、AI が生成したコードが要件を満たし、手書きのコードと同じレビューを受けていることを確認できます。

## 会話モード

**会話モード**は、エージェントにどの程度の自律性を与えるかを制御します。<kbd>Shift</kbd>+<kbd>Tab</kbd> を押すとモードを切り替えられます。

- **Interactive**: 開発者とエージェントが協力して作業します。エージェントは変更を提案し、次の操作の前に入力を待ちます。
- **Plan**: エージェントは先に計画を作成し、プロジェクトファイルを編集できません。
- **Autopilot**: エージェントは自律的にコードを書き、テストを実行し、タスクが完了するまで反復します。

まず Plan モードで計画を確認し、その後 Autopilot で実装します。

## Issue から始める

絞り込み作業の前に Codespace に戻り、リポジトリとターミナルを準備します。

1. Codespace に戻ります。停止している場合は再起動します。
2. 星評価の PR がマージ済みであることを確認します。
3. ターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
4. `main` を更新し、絞り込み作業用のブランチを作成します。

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Copilot CLI を起動します。

   ```bash
   copilot --yolo
   ```

6. <kbd>Tab</kbd> を 2 回押して **Issues** タブを開きます。
7. <kbd>A</kbd> を押してすべての Issue を表示します。
8. 矢印キーで **Allow users to filter games by category and publisher** というタイトルの Issue を選択します。
9. <kbd>C</kbd> を押して Issue をプロンプトに追加し、**Session** タブに戻ります。

プロンプトに `#7` (または同様の番号) が追加されます。`#` を使うと、GitHub 上の Issue や PR をコンテキストに含められます。

## 絞り込み機能を計画する

計画を立てると、機能の実装やタスクの実行を Copilot に任せる前に、方針を決められます。複雑な作業では、計画に時間をかけることをお勧めします。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Plan モードに切り替え、プロンプトの下に **Plan** と表示されていることを確認します。
2. 直前の手順で追加した Issue の後に、次のプロンプトを入力します。

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot はプロジェクトを調べ、最適な方法を検討して計画を作成します。

3. 絞り込みの動作について質問された場合は、希望に沿って回答します。唯一の正解はありません。
4. 計画が完成したら、<kbd>Control</kbd>+<kbd>E</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) を押して展開します。
5. 計画を上下にスクロールして確認します。
6. 自分の決定と合わない箇所があれば、Copilot に修正を依頼します。

## Autopilot を承認する

計画を確認したら、Autopilot で実装します。Autopilot は、完了したと判断するまで問題に取り組み、反復します。

1. **Accept plan and build on autopilot (recommended)** またはインストール済みバージョンで同様のラベルの選択肢を選びます。
2. プロンプトの下に **Autopilot** と表示されていることを確認します。
3. Copilot が計画に沿って反復し、コードを生成してテストを実行する様子を確認します。

> [!NOTE]
> 承認すると実装がすぐに始まる場合があります。先に計画をレビューしてください。依存関係が不足している、またはポートが競合していると報告された場合は、チェック完了と見なす前にセットアップの問題を解決してください。

## 実装をレビューして検証する

生成されたコードは、ほかのコードと同様にマージ前にレビューします。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Interactive モードに切り替え、モード表示が **Plan** または **Autopilot** ではないことを確認します。
2. `/diff` を入力し、絞り込み機能の実装とテストを確認します。
3. 結果を Issue と計画時の決定事項に照らし合わせます。
4. レビュー後、<kbd>Esc</kbd> を押して差分画面を閉じます。
5. プロジェクトのチェック結果を確認し、失敗があれば Copilot に解決を依頼します。

## 新しい機能を試す

Codespaces が転送するポートからサイトを開き、機能が動作するか確認します。

1. Copilot にアプリの起動を依頼します。

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces でポート `4321` が利用可能と表示されたら、**Open in Browser** を選択します。
3. 計画で合意したカテゴリの絞り込み、パブリッシャーの絞り込み、それらの組み合わせを試します。
4. リセット時と結果が空の場合の動作が、Issue と合意事項に沿っていることを確認します。
5. Codespace に戻り、Copilot に起動した開発サーバーを停止するよう依頼します。

## まとめと次のステップ

会話モードを使い分けて機能を構築し、レビューしました。このレッスンでは、次の操作を行いました。

- GitHub Issue から Copilot の会話を開始しました。
- Plan モードで要件を定義しました。
- Autopilot モードで機能を実装しました。
- コードをレビューしました。
- 転送されたブラウザーで機能を手動で検証しました。

次は[カスタム指示を使ってコード生成が文書化されたプラクティスに従うようにし][next-lesson]、さらに詳しく確認します。

## リソース

- [GitHub Copilot CLI の Autopilot][autopilot]
- [Copilot CLI コマンド リファレンス][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
