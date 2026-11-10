---
title: "レッスン 5 - quality-checks スキルのカスタマイズと使用"
description: "既存の quality-checks スキルを確認し、レポート形式をカスタマイズして、フィルター機能の検証に使用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

コードを書く作業には、コードを書く以上のことがあります。これまでは、手動でコードを検証し、指示ファイルを使って規約に従わせてきました。テスト、lint、継続的インテグレーション (CI) のほかの作業には、**エージェントスキル**が適しています。スキルを使うと、こうした処理を正しく実行する方法を Copilot に伝えられます。

このレッスンでは、次の内容を学習します。

- 既存の `quality-checks` スキルを確認する。
- 結果の形式をカスタマイズする。
- スキルを再読み込みして実行する。

## シナリオ

Tailspin Toys では、単体テスト、lint、型チェックに `quality-checks` スキルを使用しています。チームは、結果を読みやすくするためにレポートを改善したいと考えています。

## 指示、スクリプト、リソース

エージェントスキルは、再利用可能なタスクの指示、実行可能なスクリプト、補助リソースをまとめ、エージェントが必要なときに読み込みます。基本構成は、スキル名を付けたフォルダーと、その中の `SKILL.md` ファイルです。Markdown ファイルには、スキルの名前と説明を定義するフロントマター、概要、呼び出すタイミングのガイダンスが含まれます。スキル用のスクリプトやほかのリソースをサブフォルダーに追加することもできます。

> [!NOTE]
> スキルに追加のファイルやフォルダーは必須ではありません。Tailspin Toys の `quality-checks` スキルには、プロジェクトに既存のコマンドを使うため、`SKILL.md` だけが含まれています。

スキルは、チームで共有して再利用するリポジトリアセットとしてプロジェクトの `.github/skills` フォルダーに配置できます。また、ユーザーのスキルフォルダー `~/.copilot/skills` に配置することもできます。

## スキルを確認する

Tailspin Toys のチームが単体テスト、lint、型チェックを実行するために作成した `quality-checks` スキルを確認します。

1. Codespace に戻り、Codespaces エディターで `.github/skills/quality-checks/SKILL.md` を開きます。
2. 先頭にある `name` と `description` を読みます。説明は、Copilot がスキルをいつ呼び出すかを判断するのに役立ちます。
3. 指示を読み、テストと lint の手順を Copilot にどう案内しているかを確認します。
4. スキルには **Results output formatting** セクションがまだないことを確認します。

## 変更前にスキルを実行する

スキルは Copilot CLI から直接呼び出すか、自然言語で依頼できます。まず、3 つのチェックを実行するよう Copilot に依頼します。

1. Interactive モードでフィルター機能の会話に戻ります。
2. 次のプロンプトを送信します。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 最後に表示されるレポートを確認します。

## レポートをカスタマイズする

実行内容、成否、ツールが報告した情報を示す、より詳しいレポートに変更します。

1. `.github/skills/quality-checks/SKILL.md` に戻ります。
2. 次のセクションをファイルの末尾に追加します。

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. ファイルが自動的に保存されたことを確認します。

## 更新したスキルを実行する

スキルを変更した状態で動作を確認します。Copilot CLI は、会話を再起動せずに編集済みのスキルを再読み込みできます。

1. `/skills reload` を入力します。
2. 先ほどとまったく同じプロンプトを送信します。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 最後に表示されるレポートを確認し、最初のレポートと比較します。

## まとめと次のステップ

既存のエージェントスキルをカスタマイズして使用しました。このレッスンでは、次の作業を行いました。

- 単体テスト、lint、型チェックに使う `quality-checks` スキルを確認した。
- 結果の形式をカスタマイズした。
- スキルを再読み込みして実行した。

この変更は、フィルター機能とともに機能の PR に含めます。次は、[Model Context Protocol (MCP) を使う Playwright サーバー][next-lesson]で、Copilot がサイトを直接操作できるようにします。

## そのほかのスキル例

コミュニティの次の例は参考資料であり、追加の課題ではありません。

- [Agent Skills 仕様][skill-spec]
- [コントリビューションのワークフロー: `make-repo-contribution`][contribution-example]
- [要件ドキュメント: `prd`][prd-example]
- [図とバンドルされたエクスポートスクリプト: `drawio`][drawio-example]
- [ブラウザーテスト: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
