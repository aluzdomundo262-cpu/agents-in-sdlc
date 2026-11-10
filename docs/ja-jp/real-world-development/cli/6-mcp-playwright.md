---
title: "レッスン 6 - Playwright MCP で機能を検証する"
description: "Copilot CLI で Playwright Model Context Protocol (MCP) を確認または設定し、ブラウザーで絞り込み機能を試します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

コードを書くことだけが開発ではありません。データや外部サービスを扱い、Copilot が利用できる自動化機能を追加することもあります。MCP サーバーを使うと、Copilot CLI に組み込まれていないツールやサービスを利用できます。

このレッスンでは、次の操作を行います。

- Model Context Protocol (MCP) と Copilot CLI での利用方法を理解します。
- まだ利用できない場合は Playwright MCP サーバーを追加します。
- エージェントにブラウザーを操作させ、絞り込み機能を試します。

## シナリオ

ユニットテストとエンドツーエンドテストは重要ですが、UI の変更を検証するには、実際に UI を操作する必要があります。Copilot にサイトをユーザーのように操作させると、期待どおりに動作するかを確かめながら、変更を自動化できます。

## Model Context Protocol (MCP) とは

[Model Context Protocol (MCP)][mcp-blog-post] は、AI エージェントが外部のツールやサービスと通信するための仕組みです。MCP を利用すると、エージェントは最新の情報にアクセスし、代わりに操作を実行できます。

ツールやリソースへのアクセスは、エージェントと外部サービスをつなぐ MCP サーバーを通じて行います。各サーバーは、エージェントが利用できるツールとリソースを提供します。

- **[GitHub MCP Server][github-mcp]**: GitHub リポジトリ、Issue、プルリクエストを管理する API にアクセスします。
- **[Playwright MCP Server][playwright-mcp-server]**: Playwright を使ったブラウザー自動化機能を提供します。

ほかにも多くの MCP サーバーがあります。GitHub は、エコシステム内のサーバーを見つけて貢献できる [MCP レジストリ][mcp-registry]をホストしています。

> [!CAUTION]
> MCP サーバーも、プロジェクトのほかの依存関係と同様に扱ってください。利用前にソースコードを確認し、発行元を検証して、セキュリティへの影響を検討してください。

## Playwright MCP サーバーを追加する

まだ Playwright MCP サーバーが利用できない場合は、Copilot がユーザーのようにサイトを操作できるように追加します。

> [!NOTE]
> Copilot CLI ですでに Playwright MCP を設定している場合は、セットアップを省略して次のセクションに進みます。

1. Codespace に戻ります。
2. Copilot CLI で次のコマンドを入力し、MCP サーバー追加ダイアログを開きます。

   ```plaintext
   /mcp add
   ```

3. 名前に `playwright` と入力して <kbd>Tab</kbd> を押します。
4. サーバーの種類が **STDIO** であることを確認するため <kbd>Enter</kbd> を押し、続けて <kbd>Tab</kbd> を押します。
5. **Command** ダイアログに次の内容を貼り付けます。

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. <kbd>Control</kbd>+<kbd>S</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) を押して MCP サーバーを保存します。
7. <kbd>Esc</kbd> を押して MCP ダイアログを閉じます。

## Playwright で機能を確認する

Copilot が利用できる Playwright MCP サーバーを使って、手動で行った機能確認を自動化します。

1. 次のプロンプトを使い、Playwright MCP サーバーで絞り込み機能を検証するよう Copilot に依頼します。

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> Copilot は通常、自動的に MCP サーバーを見つけるため、明示的に指定しなくてもかまいません。使うサーバーが分かっている場合は、プロンプトに記載すると結果が安定しやすくなります。

2. Copilot がブラウザーで機能を確認する操作を実行する様子を見ます。
3. レポートを読み、期待どおりに動作していることを確認します。

Copilot はサーバーを起動し、Playwright でサイトを操作してからサーバーを停止し、結果を報告します。

## まとめと次のステップ

Playwright MCP サーバーを使い、Copilot CLI から実際のブラウザーで機能を確認しました。このレッスンでは、次の操作を行いました。

- MCP と Copilot CLI での利用方法を学びました。
- 未設定の場合に Playwright MCP サーバーを追加しました。
- エージェントにブラウザーを操作させ、絞り込み機能を試しました。

次は、スキルとブラウザーツールを専門的な役割でまとめる[QA カスタムエージェントを作成します][next-lesson]。

## リソース

- [MCP とは何か、なぜ話題になっているのか][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [Copilot CLI に MCP サーバーを追加する][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
