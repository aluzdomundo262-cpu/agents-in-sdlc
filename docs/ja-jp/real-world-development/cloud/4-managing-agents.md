---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

ここまでの演習では、ユーザー体験の改善と機能追加を目的に、Copilot cloud agent に 3 つのタスクを依頼しました。cloud agent は非同期かつ自律的に作業しますが、タスクを監視することも重要です。

GitHub.com の[エージェント ページ][agents-page]など、cloud agent に割り当てたタスクを管理するツールがあります。ここでは、オープンなプルリクエスト (PR) があるすべてのエージェント タスクを確認できます。作業内容を調べたり、進行中のセッションに追加の指示を送ったりできます。

このレッスンでは、次の操作を行います。

- エージェント ページで cloud agent のタスクを監視します。
- 進行中のセッションに追加の機能を依頼します。

## シナリオ

ハイコントラスト モードの作成を依頼した後、チームはライトモードも追加したいと考えました。サイトのスタイルと切り替え機能を変更しているため、同じ作業に含めるのが合理的です。エージェントの作業を方向付けて、両方のモードを追加します。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てたタスクの現在の状態を確認します。

1. [Copilot agents ページ](https://github.com/copilot/agents)に移動します。
2. メイン パネルと左側のパネルにあるタスク一覧を確認します。次のようなタスクが表示されます。
   - コードベースのドキュメントを更新する
   - ゲーム変更用 API を生成する
   - Web サイトにハイコントラスト モードを追加する
3. 実行中のタスクを選択し、Copilot が行った操作を確認します。次のような内容が含まれる場合があります。
   - リポジトリからコードをチェックアウトする
   - Copilot の環境を作成する
   - MCP サーバーを設定する
   - タスク完了に向けた作業を行う

> [!NOTE]
> 表示される手順は、Copilot の作業状態や進め方によって異なります。

4. 右側に表示されるプルリクエスト (PR) パネルも確認します。PR と変更されたファイルを確認して、作業を監視できます。

## cloud agent に追加の指示を送る

現在実行中のタスクを確認したので、ハイコントラスト モードに取り組むエージェントへライトモードも追加するよう依頼します。

1. ハイコントラスト モードに関するセッションを選択します。タイトルは Copilot が付けた名前や作業状態によって異なります。

   ![Mission control に表示されたアクセシビリティ セッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが完了して作業が始まるまで、数分間セッションを確認します。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを入力します。

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![Agents ページで、セッションへの追加指示ダイアログが強調表示された画面](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot が指示を受け取り、作業に加えたことを確認します。

## Copilot の作業を待つ

Copilot は、メッセージを送信した時点で実行していた手順を終えた後、更新したタスクに取り組みます。完了まで数分かかる場合があります。その間に、これまでに学んだことを振り返ってください。

## まとめと次のステップ

Copilot agents ページを使って、GitHub Copilot cloud agent のタスクを監視し、方向付けました。この Mission control では、実行中と完了済みのタスクを追跡し、作業内容を確認して、進行中のタスクに追加の指示を送れます。

- エージェント ページで cloud agent のタスクを監視しました。
- 進行中のセッションに追加の機能を依頼しました。

Copilot がアクセシビリティ機能を実装している間に、次は[作成されたプルリクエストを反復して改善します][next-lesson]。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタムエージェントについて][custom-agents]

---

| [← 前のレッスン: カスタムエージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復して改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
