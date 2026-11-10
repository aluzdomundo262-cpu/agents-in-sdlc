---
title: "レッスン 4 - カスタム指示で Copilot を導く"
description: "リポジトリの指示を確認し、ドキュメント標準を追加して、絞り込み機能のコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を使うときはコンテキストが重要です。タスクを特定の方法で進める必要がある場合、そのガイダンスを Copilot が参照できるようにします。[指示ファイル][instruction-files]には、求めるコードだけでなく、その構成方法も記述できます。絞り込み機能を実装したので、Copilot が参照した指示を確認し、ドキュメント標準を追加してコードに適用します。

このレッスンでは、次の操作を行います。

- リポジトリの指示ファイルとパスで適用範囲を限定した指示ファイルがエージェントに届く仕組みを確認します。
- コーディング標準が守られるように指示ファイルを更新します。
- 指示ファイルがコードに与える影響を確認します。

## シナリオ

Tailspin Toys には開発プラクティスのガイドラインがあります。

- コメントではコードの内容を繰り返さず、意図や自明でない決定を説明します。
- `db/` と `src/lib/` のエクスポート関数には、目的、パラメーター、戻り値を説明する TSDoc/JSDoc を記述します。該当する場合は、注入可能な `db` 引数も含めます。
- 再利用可能な Astro コンポーネントには `Props` の契約を記述し、関連コードが変わったときはコメントも更新します。
- 既存の書式設定と lint のガイダンスを維持します。

指示ファイルを使い、Copilot がこうしたプラクティスに沿って作業できるようにします。

## 指示ファイル

カスタム指示は、コーディングスタイルや要件のコンテキストを Copilot に与えます。リポジトリ全体に適用する指示も、特定の種類のファイルに適用する指示も作成できます。

指示ファイルには次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリへのすべてのリクエストで Copilot に送られる指示ファイルです。多くのリクエストに関係するプロジェクト全体の情報を記載します。
- `.github/instructions/*.instructions.md` は、特定の言語、ファイル種類、タスクに適用するガイドラインを記載します。

> [!NOTE]
> ほかの形式の指示とそのサポート状況は、環境によって異なります。形式に依存する前に、[カスタム指示のサポート リファレンス][custom-instructions-support]を確認してください。

## プロジェクトのカスタム指示ファイルを確認する

スターター プロジェクトに含まれる指示ファイルを調べ、変更する前に内容を確認します。

1. Codespace に戻ります。
2. Codespaces エディターで `.github/copilot-instructions.md` を開き、プロジェクトの簡単な説明と、このリポジトリのすべての Copilot 操作に適用されるガイダンスを確認します。
3. `.github/instructions` フォルダーを開き、Astro、Drizzle データ層、テストなどの指示ファイルを確認します。
4. `.github/instructions/unit-tests.instructions.md` を開き、先頭の `applyTo` が指示の適用対象を決める glob であることを確認します。
5. `.github/instructions/drizzle.instructions.md` を開き、ほかの指示ファイルや既存プロジェクト ファイルへのリンクを確認します。大きな指示を再利用可能な小さなファイルに分け、例を参照させることができます。

## チームのガイダンスに合わせて指示ファイルを更新する

既存の指示に、生成する TypeScript の TSDoc コメントに関するルールを追加します。

1. `.github/copilot-instructions.md` の **Code formatting guidance** セクションを探します。およそ 35 行目にあります。
2. 次の項目を最後の箇条書きとして追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

変更は自動的に保存されます。

## 更新したガイダンスを適用する

Copilot CLI は会話の開始時にリポジトリの指示を読み込みます。更新した指示を使うため、絞り込みの会話を閉じて再開します。

1. 絞り込みの会話が開いている場合は `/exit` を入力します。会話は自動的に保存されます。
2. リポジトリのルートで `game-filters-cli` ブランチに切り替えてから、保存済みの会話を再開します。

   ```bash
   copilot --resume
   ```

   選択を求められた場合は、絞り込みの会話を選び、`game-filters-cli` ブランチがチェックアウトされていることを確認します。

3. 次のプロンプトで更新したガイダンスを適用します。

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. `/diff` を入力し、変更された TypeScript ファイルを確認します。新しい TSDoc コメントがコードを正確に説明していることを確認します。

## まとめと次のステップ

Copilot CLI が指示ファイルからコンテキストを取得する方法を確認し、新しい標準を機能に適用しました。このレッスンでは、次の操作を行いました。

- リポジトリの指示ファイルとパスで適用範囲を限定した指示ファイルがエージェントに届く仕組みを確認しました。
- 指示ファイルを更新してコーディング標準を追加しました。
- 指示ファイルがコードに与える影響を確認しました。

次は[再利用可能な quality-checks スキルをカスタマイズして実行し][next-lesson]、lint とテストを一貫して実施します。

## リソース

- [Copilot CLI のカスタム指示を追加する][instruction-files]
- [カスタム指示のサポート][custom-instructions-support]
- [効果的なカスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [Awesome Copilot — 指示ファイルなどのリソース集][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
