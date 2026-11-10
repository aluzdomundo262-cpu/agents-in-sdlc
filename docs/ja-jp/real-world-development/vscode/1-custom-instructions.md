---
title: "演習 1 - カスタム指示 (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: エージェントモード →][next-lesson]

生成型の人工知能 (AI) を使うときは、コンテキストが重要です。タスクの進め方に決まりがある場合や、Copilot に知っておいてほしい背景情報がある場合は、その情報を参照できるようにします。コンテキストを共有する方法はいくつかあります。中でも[指示ファイル][instruction-files]は、コード生成の指針を Copilot に伝える方法です。

この演習では、次のことを行います。

- リポジトリのカスタム指示とパスを対象とする指示ファイルを使い、プロジェクト固有のコンテキスト、コーディングガイドライン、ドキュメント標準が Copilot にどう伝わるかを確認します。
- 現在の指示を適用した状態で、フィルター機能の最初のデータ部分となる publishers ヘルパーを生成します。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加します。
- 同じプロンプトを再実行し、生成コードが新しい標準に従う様子を確認します。
- 指示の更新とフィルター機能のデータ部分を `main` にコミットし、次の演習で Copilot が最新の指示を使えるようにします。

> [!CAUTION]
> 生成コードが設定した標準から外れる場合があります。Copilot の出力は確率的に変わるためです。この演習では、出力を一字一句同じにするのではなく、指示の更新後にコードが標準に従う傾向を確認します。

## 指示ファイル

### シナリオ

Tailspin Toys には、開発に関するガイドラインと要件があります。

- データ層には必ず単体テストを用意します。
- ユーザーインターフェイス (UI) はダークモードにし、現代的な見た目にします。
- コードには TSDoc のドキュメントコメントを追加します。
- 各ファイルの先頭に、そのファイルの役割を説明するコメントブロックを追加します。

指示ファイルを使って、Copilot がこれらの開発方針に沿ってタスクを進められるようにします。

### カスタム指示

カスタム指示を使うと、コーディングスタイルや要件に関するコンテキストを Copilot に伝えられます。好みの規約、ライブラリ、コードに含めたいコメントの種類などを指定でき、より適切な提案やコードスニペットを得るのに役立ちます。リポジトリ全体、またはタスクに応じたファイルの種類に指示を設定できます。

指示ファイルには次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリに関するすべてのリクエストで Copilot に送信される単一の指示ファイルです。技術スタック、開発対象の概要、ベストプラクティス、全般的なガイダンスなど、Copilot Chat や CLI へのほとんどのリクエストに関係する情報を記載します。
- `.github/instructions/*.instructions.md` は、特定のタスクやファイルの種類に関する指針を記載するファイルです。TypeScript や Astro などの言語、UI コンポーネントや単体テストの作成などのタスクに使用できます。

> [!NOTE]
> 統合開発環境 (IDE) で作業する場合、指示ファイルは Copilot Chat のコード生成にのみ使われます。コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、リポジトリレベルの指示と `applyTo` フロントマターを持つ `*.instructions.md` ファイルの両方を使ってコードを生成します。
>
> Copilot は AGENTS.md や CLAUDE.md など、ほかの規格に基づく指示ファイルにも対応しています。[対応する指示ファイルの規格][custom-instructions-support]を確認してください。

### 指示ファイルを管理するためのベストプラクティス

指示ファイルの作成について詳しく説明することはこの演習の範囲外ですが、サンプルプロジェクトには代表的な構成例があります。基本的には、次のように管理します。

- `copilot-instructions.md` には、開発対象の説明、プロジェクト構成、全体に適用するコーディング標準など、プロジェクトレベルの情報を記載します。
- `*.instructions.md` には、単体テスト、Astro コンポーネント、データ層などのファイル種類や特定のタスクに関する指針を記載します。
- 自然な言葉で、明確なガイダンスとコードの良い例・悪い例を示します。

指示ファイルの作り方や AI の使い方に唯一の正解はありません。実際に試しながら、プロジェクトに合う方法を見つけてください。

> [!TIP]
> GitHub Copilot を使うプロジェクトには、十分な指示ファイルを用意することをお勧めします。このプロジェクトには、[UI 更新用][ui-instructions]や [Astro 用][astro-instructions]など、さまざまなタスク向けのファイルがあります。
>
> Copilot に指示ファイルを作成させることもできます。操作方法は利用する環境によって異なります。たとえば VS Code では **Configure Chat → Generate Agent Instructions**、Copilot CLI では `/init` を使います。各環境の演習では、必要な場合に操作方法を説明します。
>
> テンプレートや出発点を探す場合は、指示ファイル、カスタムエージェント、その他のリソースを集めた [awesome-copilot][awesome-copilot] を確認してください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム指示ファイルを確認する

このリポジトリには、中心となる `copilot-instructions.md` と、タスクごとの `*.instructions.md` ファイルがあります。エディターまたは GitHub の Web UI で内容を確認します。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの簡単な説明と、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** にある **GitHub Actions Workflows** の補足ガイダンスも確認してください。これらの情報は Copilot とのやり取り全般に適用されます。
3. `.github/instructions` フォルダーを開いて内容を確認します。Astro ファイル、Drizzle データ層、テストなどの指示ファイルがあります。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドが、リポジトリのルートからの glob パターンを指定しています。この例では、`**/*.test.ts` に一致する TypeScript のテストファイルが対象です。
5. このプロジェクトの単体テスト作成に関する指示を確認します。
6. `.github/instructions/drizzle.instructions.md` を開き、末尾までスクロールします。`unit-tests.instructions.md` などの指示ファイルや、プロジェクトの既存ファイルへのリンクがあります。パスはリポジトリのルートではなく、指示ファイルの場所からの相対パスです。これにより、指示を小さな再利用可能なファイルに分け、Copilot が参考にできる例を示せます。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはプロジェクトのコーディング標準が記載されていますが、コード内のドキュメントコメントはまだ必須ではありません。次の手順で、TSDoc のドキュメントコメントとファイル先頭のコメントヘッダーに関する規則を追加します。

## 変更用ブランチを作成する

変更を分けて管理するため、新しいブランチを作成します。

1. 前の演習で使った codespace に戻ります。
2. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して、新しいターミナルを開きます。
3. 次のコマンドを実行してブランチを作成し、切り替えます。

   ```bash
   git checkout -b custom-instructions
   ```

## 指示を更新する前に Copilot Chat を使う

> [!TIP]
> **Copilot Chat を開く**
>
> 以下の手順で新しい会話を始めます。モードとモデルの選択は演習ごとに異なるため、該当する手順で説明します。
>
> 1. codespace に戻ります。
> 2. Copilot Chat パネルを開きます。
> 3. **New Chat** を選択します。

カスタム指示の効果を確認するため、まず現在の指示ファイルを適用した状態でプロンプトを送信します。その後、指示を更新して同じプロンプトを再送信し、違いを確認します。

1. 前の演習で開いたエディタータブを閉じ、Copilot が必要なコンテキストだけを参照できるようにします。
2. ヘルパーを配置するファイルとして `src/lib/publishers.ts` を開きます。
3. Chat ビューのエージェントのドロップダウンで **Agent** を選択し、Copilot がファイルを変更できるようにします。

   ![Chat ビューのエージェント選択メニューを示すスクリーンショット。](../../../_images/shared-chat-mode-selector.png)

4. 次のプロンプトを送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot がプロジェクトを調べ、ヘルパーファイルとテストなどにコードの変更を適用する様子を確認します。
6. 提案されたヘルパーが、型付きの関数であることを確認します。最初の引数として `db` クライアントを受け取り、型付きの出版社配列を返します。これは `src/lib/*.ts` に適用される `.github/instructions/drizzle.instructions.md` のデータ層の規約によるものです。
7. 提案されたコードに TSDoc のドキュメントコメントとファイルレベルのコメントヘッダーがないことを確認します。

> [!CAUTION]
> Copilot は確率的に動作するため、指示がなくてもドキュメントコメントを追加することがあります。その場合も問題ありません。指示を更新した後に一貫性が高まることが、この演習のポイントです。

## リポジトリ全体に適用する標準を追加する

先ほど確認したように、`.github/copilot-instructions.md` はプロジェクトレベルの情報を Copilot に伝えるファイルです。コード提案の質を高めるため、リポジトリのコーディング標準に新しい規則を加えます。

1. `.github/copilot-instructions.md` を開き直します。
2. 27 行目付近にある **Code formatting requirements** セクションを探します。現在の標準を確認し、コード内のドキュメントに関する規則がまだないことを確かめます。
3. 既存の標準の直下に、次の Markdown を追加します。ファイルヘッダーと TSDoc コメントを Copilot に求める規則です。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 指示ファイルは、リポジトリ全体に適用する `.github/copilot-instructions.md` と、特定の言語、ファイル種類、タスクに適用する `*.instructions.md` のどちらにも作成できます。ドキュメントコメントの規則のようなプロジェクト全体の標準には、リポジトリレベルのファイルが適しています。

## 同じプロンプトを再実行して違いを確認する

リポジトリ全体に適用する標準がコード生成に反映されることを確認するため、先ほどと同じプロンプトを再度送信します。

1. Copilot Chat に戻り、**New Chat** を選択して会話を新しくします。
2. `src/lib/publishers.ts` をもう一度開き、Copilot が適切なファイルに注目できるようにします。
3. 先ほどと**同じプロンプト**を送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 提案されたファイルの先頭に、次のようなコメントブロックがあることを確認します。

   ```typescript
   /**
    * Tailspin Toys クラウドファンディングプラットフォームの出版社データアクセス用ヘルパーです。
    * データベースから出版社情報を取得する関数を提供します。
    */
   ```

5. 提案された関数に、次のような TSDoc コメントがあることを確認します。

   ```typescript
   /**
    * ID と名前を含むすべての出版社の一覧を返します。
    *
    * @param db - Drizzle データベースクライアントです。
    * @returns 出版社オブジェクトの配列に解決される Promise です。
    */
   ```

新しいプロジェクト標準を Copilot に伝え、次の演習で使う実際のコードに適用しました。

## 指示と変更をコミットしてブランチをプッシュする

指示ファイルもほかの資産と同じようにソース管理します。変更内容を確認してコミットし、ブランチをリポジトリにプッシュします。

1. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押し、新しいターミナルを開きます。
2. 次のコマンドを実行し、指示とヘルパーの変更があることを確認します。

   ```bash
   git status
   ```

3. 次のコマンドで指示の更新とヘルパーの基礎部分をステージしてコミットします。Copilot がテストなどの追加ファイルを変更していて `git status` に表示される場合は、それらも追加します。

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # git status にテストなどの追加変更が表示された場合は、それらのファイルも追加します。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. 次のコマンドでブランチをリポジトリにプッシュします。

   ```bash
   git push -u origin custom-instructions
   ```

## プルリクエストを作成してマージする

ブランチをプッシュしたら、バックログにあるドキュメント標準の Issue に関連付けてプルリクエスト (PR) を作成します。GitHub ツールはすでにプロジェクトに接続されているため、Copilot に Issue を探し、Issue を完了する PR を作成してマージするよう依頼できます。

> [!NOTE]
> この演習では初めて Copilot に GitHub 上の操作を依頼します。プロジェクトテンプレートには GitHub のツールがあらかじめ設定されているため、追加のセットアップは不要です。Copilot が初めてツールを使うときに、VS Code で GitHub へのサインインを求められる場合があります。案内に従って認証してください。この接続の仕組みである Model Context Protocol (MCP) については、後の演習で説明します。

1. codespace で Copilot Chat を開きます。
2. <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) を押して Copilot Chat ビューを開き、エージェントのドロップダウンで **Agent** が選択されていることを確認します。
3. Copilot に、指示ファイルの更新に関する Issue を探し、現在のブランチから PR を作成するよう依頼します。PR には指示の更新と、今後のフィルター機能に向けた publishers ヘルパーの基礎部分の両方を記載するよう伝えます。

   ```text
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot が Issue を探して PR を作成する様子を確認します。
5. Copilot が GitHub 操作の許可を求めたら、コマンドを確認して、適切な操作だけに **Allow** を選択します。
6. PR が作成されたら、次のプロンプトでマージと、ローカルで `main` に戻って最新の変更を取得するよう依頼します。

   ```text
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. Copilot が GitHub 操作やシェルコマンドの許可を求めたら、内容を確認し、適切な操作だけに **Allow** を選択します。

これで GitHub Copilot を使って PR を作成し、マージできました。

## まとめと次のステップ

プロジェクトの指示ファイルから Copilot がコンテキストを得る方法を確認し、Copilot Chat を使って次の作業を行いました。

- リポジトリとパスを対象とする指示ファイルが、プロジェクトのコンテキスト、コーディングガイドライン、ドキュメント標準を Copilot に伝える方法を確認しました。
- 現在の指示を適用した状態で、フィルター機能の最初のデータ部分となる publishers ヘルパーを生成しました。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加しました。
- 同じプロンプトを再実行し、提案されたコードが新しい標準に従うことを確認しました。
- 指示の更新とフィルター機能のデータ部分を `main` にコミットし、次の演習で Copilot が最新の指示を使えるようにしました。

次は[エージェントモード][next-lesson]を使い、Copilot にコードベース全体にわたる新機能を追加させます。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベストプラクティス][instructions-best-practices]
- [Copilot 向けのより良いカスタム指示を書く 5 つのヒント][copilot-instructions-five-tips]
- [GitHub Copilot の個人用カスタム指示][personal-instructions]
- [awesome-copilot — 指示ファイルなどのリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
