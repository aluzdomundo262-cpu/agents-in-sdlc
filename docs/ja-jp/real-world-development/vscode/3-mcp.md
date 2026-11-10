---
title: "演習 3 - Playwright Model Context Protocol (MCP) サーバーで機能をテストする"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: エージェントモード][previous-lesson] · [次のレッスン: カスタムエージェント →][next-lesson]

エージェントモードでフィルター機能を実装しました。プルリクエスト (PR) を作成する前に、ブラウザーで動作を確認します。自分でアプリを操作する代わりに、**Playwright MCP サーバー**を接続し、Copilot に実際のブラウザーを操作させて機能をテストしてから、ブランチを公開して PR を作成します。

この演習では、次のことを行います。

- Model Context Protocol (MCP) と、MCP サーバーが新しいツールで Copilot を拡張する仕組みを確認します。
- Playwright MCP サーバーをワークスペースに追加します。
- Copilot にサーバーを使わせ、ブラウザーでフィルター機能を手動テストします。
- フィルター機能のブランチを公開し、プルリクエストを作成します。

## Model Context Protocol (MCP) とは

エージェントモードは、エディターの外部にアクセスできると、さらに多くの作業をこなせます。Copilot が外部ツールやサービスと通信するための標準が Model Context Protocol (MCP) です。

![エージェントモードがコンテキスト、大規模言語モデル (LLM)、ツール、MCP サーバーや VS Code 拡張機能が提供するツールと連携する仕組みを示す図](../../../_images/ex1-mcp-diagram.png)

[Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) は、人工知能 (AI) エージェントが外部のツールやサービスと通信するための仕組みです。MCP を使うと、AI エージェントはリソースを通じて最新情報にアクセスしたり、ツールを通じて開発者に代わって操作を実行したりできます。

ツールやリソースには、AI エージェントと外部ツールやサービスをつなぐ MCP サーバーを介してアクセスします。MCP サーバーは、既存のアプリケーションプログラミングインターフェイス (API) や npm パッケージのようなローカルツールなどと、AI エージェントとの通信を管理します。各 MCP サーバーが、エージェントから利用できるツールやリソースを提供します。

よく使われる MCP サーバーには、次のものがあります。

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)**: GitHub リポジトリを管理するための API を提供します。新しいリポジトリの作成、既存リポジトリの更新、Issue やプルリクエストの管理などをエージェントが実行できます。
- **[Playwright MCP Server](https://github.com/microsoft/playwright-mcp)**: Playwright を使ったブラウザー自動化機能を提供します。Web ページへの移動、フォームへの入力、ボタンの選択などをエージェントが実行できます。

ほかにも、さまざまなツールを提供する MCP サーバーがあります。GitHub が運営する [MCP レジストリ](https://github.com/mcp)で、エコシステム内のサーバーを見つけたり、登録に貢献したりできます。

> [!CAUTION]
> MCP サーバーは、プロジェクトのほかの依存関係と同じように扱ってください。
>
> 1. 利用前にソースコードをよく確認し、発行元を確かめ、セキュリティへの影響を検討します。
> 2. 信頼できる MCP サーバーだけを使い、機密リソースや操作へのアクセスを許可する際は注意してください。

## MCP の構成を確認する

`.vscode/mcp.json` ファイルで、この VS Code ワークスペースから利用できる MCP サーバーを設定します。

1. codespace で `.vscode/mcp.json` を開きます。
2. 次のように、`github` サーバーがすでに設定されていることを確認します。

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

この `github` エントリはプロジェクトテンプレートに含まれています。そのため、前の演習で Copilot が Issue のバックログを読み取れました。このサーバーは[リモート GitHub MCP サーバー][remote-github-mcp-server]を使います。ローカルにインストールする必要はありません。VS Code は Hypertext Transfer Protocol (HTTP) 経由で接続し、Copilot が初めてツールを使うときに GitHub で認証します。

## Playwright MCP サーバーを追加する

次に、2 つ目のサーバーを追加します。[Playwright MCP サーバー][playwright-mcp-server]を使うと、Copilot がブラウザーを操作できるため、実装した機能をテストできます。

1. `.vscode/mcp.json` で `github` と並べて `playwright` エントリを追加し、ファイルを次のようにします。

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. ファイルを保存します。

リモートの `github` サーバーと異なり、`playwright` はローカルサーバーです。VS Code が `npx @playwright/mcp@latest` を実行して起動します。`--headless` フラグを使うと、Playwright は画面に表示しないブラウザーを実行します。デスクトップ環境がない codespace では、この設定が必要です。

> [!NOTE]
> Tailspin Toys プロジェクトはエンドツーエンドテストに Playwright を使っているため、必要なブラウザーは通常すでにインストールされています。Copilot がブラウザーが見つからないと報告した場合は、次の手順で Chromium をインストールして再試行します。
>
> 1. Copilot に `npx playwright install chromium` を実行するよう依頼します。
> 2. もう一度テストします。

## サーバーを起動して信頼する

VS Code は、Copilot がサーバーのツールを初めて必要としたときに MCP サーバーを起動します。その際、サーバーを信頼するかどうか確認されます。

1. `.vscode/mcp.json` で `playwright` エントリの上に表示される **Start** を選択し、サーバーを起動して設定が正しいことを確認します。
2. VS Code からサーバーを信頼するか確認されたら、構成を確認して、起動を許可します。

手動で起動する必要はありません。ここで起動しない場合は、次の手順で Copilot がツールを使うときに VS Code が起動し、信頼を確認します。

## フィルター機能をテストする

[Playwright MCP サーバー][playwright-mcp-server]が接続されると、Copilot が実際のブラウザーを操作できます。開発者がアプリを手動で操作しなくても、エージェントがページを開き、移動し、フィルターを適用し、結果を読み取って要約します。会話を続けながら機能の動作をすばやく確認できます。

Playwright MCP サーバーは、スクリーンショットではなく、ページの[アクセシビリティツリー][playwright-mcp-server]を使います。エージェントはボタン、リンク、リスト項目などのラベル付き要素を通じてページを確認します。これは支援技術と同じ仕組みを使うため、機能テストと同時に簡単なアクセシビリティ確認もできます。

サーバーを接続し、アプリを起動した状態で、次のプロンプトを Copilot に送信してフィルター機能をテストします。

1. 次のプロンプトを送信します。

   ```text
   Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

   1. Go to the games page and note how many games are listed.
   2. Apply a category filter and confirm the list updates to only show games in that category.
   3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
   4. Combine a category and a publisher filter and confirm the results respect both.

   Report what you observe at each step, and call out anything that does not behave as expected.
   ```

2. Copilot が Playwright MCP サーバーを通じてブラウザーを起動し、各手順を実行して結果を報告することを確認します。報告内容を Issue の受け入れ基準と照らし合わせます。動作に問題があれば、追加の質問をするか、プルリクエストを作成する前にコードを修正するよう依頼します。

> [!NOTE]
> このテストには、アプリを `http://localhost:4321` で実行しておく必要があります。開発サーバーを停止している場合は、次の手順で再起動します。Copilot が初めて Playwright MCP サーバーを使うときにブラウザーのダウンロードが必要になる場合があります。ブラウザーが見つからないと報告された場合は Chromium をインストールして再試行します。
>
> 1. ターミナルで `npm run dev` を実行します。
> 2. 必要な場合は、Copilot に `npx playwright install chromium` を実行するよう依頼します。

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## ブランチを公開してプルリクエストを作成する

機能の動作を確認したら、チームでレビューできるようにプルリクエスト (PR) を作成します。まず `filtering-vscode` ブランチを公開します。

1. codespace で **Source Control** パネルを開き、Copilot が行った変更を確認します。
2. **+** アイコンを選択して変更をステージします。
3. **Sparkle** ボタンでコミットメッセージを生成します。

   ![変更内容が表示された Source Control パネルのスクリーンショット](../../../_images/ex3-source-control-changes.png)

4. **Publish** を選択して、ブランチをリポジトリにプッシュします。

## プルリクエストを作成する

github.com や GitHub コマンドラインインターフェイス (CLI) など、プルリクエストを作成する方法はいくつかあります。この演習では GitHub Copilot に作成を依頼します。Copilot は関連する Issue を見つけ、PR と関連付けられます。

1. Copilot Chat パネルに移動し、**New Chat** を選択して新しいセッションを始めます。
2. エージェントのドロップダウンで **Agent** が選択されていることを確認します。これにより、Copilot が GitHub ツールを使えます。
3. 次のプロンプトを Copilot に送信して、PR を作成します。

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. Copilot が情報を集めて操作を行う際に、必要に応じて **Continue** を選択して許可します。GitHub ツールを初めて使うときは、GitHub への認証を求められる場合があります。画面の案内に従います。
5. Copilot が Issue を検索し、該当する Issue を見つけて PR を作成する様子を確認します。
6. Copilot が生成したリンクを選択し、プルリクエストをレビューします。まだマージしないでください。

## まとめと次のステップ

この演習では、次のことを行いました。

- Model Context Protocol (MCP) と、MCP サーバーが新しいツールで Copilot を拡張する仕組みを確認しました。
- Playwright MCP サーバーをワークスペースに追加しました。
- ブラウザーでフィルター機能を手動テストしました。
- ブランチを公開し、フィルター機能のプルリクエストを作成しました。

MCP サーバーを使って機能をテストしましたが、Copilot を拡張する方法は MCP だけではありません。次は[カスタムエージェントを作成し][next-lesson]、アクセシビリティレビューなど、対象を絞ったタスクを効率化します。

## リソース

- [MCP とは何か、なぜ話題になっているのか][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [GitHub MCP Server][github-mcp-server]
- [GitHub MCP レジストリ][mcp-registry]
- [VS Code の MCP サーバー][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
