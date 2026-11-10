---
title: "演習 2 - Copilot エージェントモードで機能を追加する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

小さなアプリケーションの変更でも、複数のファイルを更新したり、テストを実行したりする必要があります。開発では、関連ファイルを探し、変更を加え、テストを実行し、問題をデバッグし、更新し忘れたファイルを見つけて、さらに修正することがあります。こうした作業が続く場合もあります。

このような場面で役立つのが Copilot のエージェントモードです。

エージェントモードは、統合開発環境 (IDE) 内で、より自律的に作業するよう設計されています。開発者と同じように、まずプロジェクト構成を調べ、必要なファイルを更新し、テストなどのタスクを実行し、見つかった問題を自動的に修正します。この演習では、エージェントモードでサイトに機能を追加します。

> [!NOTE]
> 名前は似ていますが、エージェントモードとクラウドエージェントは異なる体験を提供します。エージェントモードは IDE 内で作業し、すばやいフィードバックと対話を可能にします。クラウドエージェントはチームの一員のように非同期で作業し、Issue やプルリクエストを通じてやり取りします。

この演習では、次のことを行います。

- Copilot のエージェントモードがプロジェクトを調べ、関連ファイルを特定し、複数のファイルを連携して変更する様子を確認します。
- エージェントモードでユーザーインターフェイス (UI) とデータ層にまたがる機能を実装します。
- Copilot が生成した変更とテストをレビューしてから、コードベースにマージします。

## シナリオ

ゲームの一覧が増えてきたため、カテゴリとパブリッシャーで絞り込めるようにします。前の演習では publishers ヘルパーを追加しました。この演習では Copilot のエージェントモードを使い、残りのデータ層、UI、テストの作業を完了します。

## Tailspin Toys の Web サイトを実行する

変更を加える前に、Tailspin Toys の現在の機能を確認します。

この Web サイトは、開発者をテーマにしたボードゲームのクラウドファンディングプラットフォームです。ゲームの一覧と詳細を表示します。単一の Astro アプリで、ビルド時に静的な HyperText Markup Language (HTML) を生成します。ページは frontmatter 内から Drizzle のオブジェクトリレーショナルマッピング (ORM) を使ってローカルの SQLite データベースに直接クエリするため、独立したバックエンドのアプリケーションプログラミングインターフェイス (API) や、クライアント側の UI フレームワークはありません。再利用可能なデータアクセスヘルパーは `src/lib/` にあり、必要なインタラクティブ機能は標準の Document Object Model (DOM) API を使う小規模な Astro `<script>` で追加します。

### Web サイトを起動する

`npm run dev` タスクを使うと、単一の Astro 開発サーバーを起動できます。次の手順で GitHub Codespace 上のサイトを実行します。

1. 前の演習の後に `main` に戻っていることを確認し、codespace に戻ります。
2. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して、Codespace 内に新しいターミナルを開きます。
3. 次のコマンドを実行して、フィルター機能用のブランチを作成し、切り替えます。

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 次のコマンドを実行して、Web サイトを起動します。

   ```bash
   npm run dev
   ```

   Astro 開発サーバーの準備ができると、次のような Uniform Resource Locator (URL) が表示されます。

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> ブラウザーで `http://localhost:4321` を開くダイアログが表示された場合は、次の操作で閉じます。
>
> 1. ダイアログの **x** を選択します。

5. ターミナルに表示された Astro サーバーのアドレス `http://localhost:4321` を、Mac では <kbd>Command</kbd> キー、Windows/Linux では <kbd>Ctrl</kbd> キーを押しながら選択して、Web サイトを開きます。

> [!NOTE]
> codespace のターミナルで localhost の URL を選択すると、自動的に `https://<your-codespace-name>-4321.app.github.dev/` に転送されます。これは、Web サーバーを実行している codespace へのプライベートなトンネルです。

### Web サイトを確認する

サイトを起動したら、主なページを開いて機能を確認します。

1. **Home Page** を開き、ボードゲームのタイトル、画像、説明の一覧を確認します。
2. ゲームを選択して **Game Details Page** を開き、タイトル、説明、パブリッシャー、カテゴリなどの詳細を確認します。

## Copilot でバックログを確認する

> [!TIP]
> **Copilot Chat を開く**
>
> 以下の手順で新しい会話を始めます。モードとモデルの選択は演習ごとに異なるため、該当する手順で説明します。
>
> 1. codespace に戻ります。
> 2. Copilot Chat パネルを開きます。
> 3. **New Chat** を選択します。

Web サイトの初期実装は機能しますが、さらに機能を追加します。テンプレートからプロジェクトを作成すると、Issue のバックログも自動的に作成されています。GitHub Copilot にバックログを表示するよう依頼します。

1. Chat ビューのエージェントのドロップダウンで **Agent** を選択します。エージェントはファイルを調べて変更を計画・実装し、ターミナルコマンドを実行してツールを呼び出します。

   ![Chat ビューのエージェント選択メニューを示すスクリーンショット。](../../../_images/shared-chat-mode-selector.png)

2. 使用可能なモデルの一覧から **Claude Sonnet 4.5** を選択します。

> [!CAUTION]
> このワークショップは、特定のモデルを推奨するものではありません。作成時に Claude Sonnet 4.5 を使用したため、手順にも記載しています。提案の一貫性を高め、演習を進めやすくすることを意図しています。ただし、大規模言語モデル (LLM) の出力は確率的に変わるため、提案内容が手順の説明と異なる場合があります。これは通常の動作です。

> [!NOTE]
> Copilot が別の Model Context Protocol (MCP) コマンドを使う場合がありますが、タスクを完了できるはずです。

3. 次のプロンプトを Copilot に送信して、Issue のバックログを確認します。

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. Issue を一覧表示するコマンドを実行するには **Continue** を選択します。
5. 生成された Issue の一覧と、Copilot がユーザーに役立つと判断した項目の優先順位を確認します。

## 指示ファイルを確認する

コードの生成を依頼する前に、Copilot にコンテキストを与える指示ファイルを確認します。ここでは、Web サイトへの機能追加方法に関する情報を含む[ユーザーインターフェイス (UI) 指示ファイル][ui-instructions]を使います。

1. codespace で `.github/instructions/ui.instructions.md` を開きます。
2. 機能追加の進め方に関する全体的なガイダンスを確認します。次の内容が含まれます。
   - アーキテクチャの概要。
   - コンポーネントの設計、テスト容易性、アクセシビリティの原則。
   - Astro、Cascading Style Sheets (CSS) のユーティリティフレームワーク Tailwind CSS、Drizzle などのファイル種類ごとの指示ファイルへのリンク。

> [!TIP]
> 指示ファイルから、ほかの指示ファイルやプロジェクト内のファイルを参照できます。パスは指示ファイルの場所からの相対パスです。指示を再利用可能な小さな単位に分けたり、例やテンプレートを示したりできます。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md

## フィルター機能を実装する

フィルター機能を完成させるには、少なくとも次の 3 つを変更します。

1. データ層 (`src/lib/`) のフィルターロジックを追加または調整します。
2. フィルター動作のテストを追加または更新します。
3. ゲーム一覧ページにフィルター UI を追加します。

さらに、コードベースにマージする前にテストを実行し、すべて合格する必要があります。Copilot のエージェントモードにこれらの作業を依頼します。

1. 現在の会話を続けるか、**New Chat** を選択して新しい会話を始めます。
2. **Add Context**、**Instructions**、**ui** の順に選択して、指示ファイルを追加します。

   ![UI 指示ファイルを選択する例を示すスクリーンショット](../../../_images/ex3-select-instructions-file.png)

3. Chat ビューのエージェントのドロップダウンで **Agent** が選択されていることを確認します。

   ![Chat ビューのエージェント選択メニューを示すスクリーンショット。](../../../_images/shared-chat-mode-selector.png)

4. モデルが引き続き **Claude Sonnet 4.5** であることを確認します。
5. バックログ内の関連 Issue の要件に基づいて機能を実装するよう、次のプロンプトを Copilot に送信します。

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Copilot がプロジェクトを調べて関連ファイルを特定し、データ層のヘルパー、UI、テストを変更してテストを実行する様子を確認します。

   ![Copilot がプロジェクトのファイルを調べる様子を示すスクリーンショット](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot はプロジェクトを調べ、ファイルを変更し、テストを実行するなど、複数の作業を行います。コードベースの複雑さによっては、数分かかることがあります。作業中にエディターに **Keep** と **Undo** が表示される場合があります。Copilot が作業を終えると、すべての変更に対して **Keep** または **Undo** を選べるため、作業中に操作する必要はありません。

7. Copilot から求められたら、**Continue** を選択してテストを実行します。

   ![テストの実行を確認する Copilot Chat のダイアログを示すスクリーンショット](../../../_images/ex3-agent-mode-run-tests.png)

8. 作業中に一時停止したり、テストが失敗したりすることがあります。Copilot は、タスクを完了してエラーがないと判断するまで、コード生成とテストを繰り返します。

   ![Copilot エージェントモードのチャットセッションを示すスクリーンショット](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 生成されたコードに問題がないか確認します。

> [!CAUTION]
> Copilot やほかの人工知能 (AI) ツールが生成したコードには、問題が含まれることがあります。
>
> 1. 生成されたコードを必ずレビューします。

10. Web サイトを表示しているブラウザーに戻り、新しい機能を試します。
11. 動作とコードを確認したら、Copilot Chat ウィンドウで **Keep** を選択します。

## まとめと次のステップ

GitHub Copilot のエージェントモードを使い、Tailspin Toys の Web サイトに機能を追加しました。

- エージェントモードで UI とデータ層にまたがる機能を実装しました。
- プロジェクトを調べ、関連ファイルを特定し、複数のファイルを連携して変更する様子を確認しました。
- コードベースにマージする前に、生成された変更とテストをレビューしました。

次は [Playwright MCP サーバーで機能をテストし][next-lesson]、プルリクエストを作成します。

### 追加演習 - ページングを実装する

ゲームの一覧が増えると、ページングが必要になる場合があります。この演習で学んだことを使い、Copilot にページングを追加するよう依頼してみてください。

1. 既存の指示ファイルを使うなど、現在のベストプラクティスに従います。
2. ページサイズをユーザーが選べるようにするか、固定するかを決めます。
3. 希望する実装に必要な情報を含むプロンプトを作成します。
4. Copilot に追加の変更を依頼し、コンテキストを与えながら何度か調整します。これは Copilot を使う通常の作業です。

## リソース

- [Copilot の Ask、Edit、Agent モードの違いと使い分け][choose-mode]
- [VS Code のエージェントモード][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
