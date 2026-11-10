---
title: "演習 5: GitHub Copilot の作業を反復して改善する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

## 作業をレビューする

このワークショップでは、ユーザー体験の改善と機能追加を目的に、GitHub Copilot と複数のタスクに取り組みました。コードへのドキュメント追加、デザイン チーム向けの関連ゲーム機能、ハイコントラストとライトモードによるアクセシビリティ機能を依頼しました。コード変更を確認し、必要に応じて Copilot にフィードバックを送ります。

### シナリオ

生成 AI を利用しても、ソフトウェア設計と開発・運用 (DevOps) の基本は変わりません。生成されたコードをレビューし、通常の DevOps プロセスに従います。チームがレビューできるようにする前に、ドキュメント、関連ゲーム機能、アクセシビリティ機能の提案を確認します。

## GitHub Copilot cloud agent のセキュリティ

Copilot cloud agent は非同期かつ監視なしで作業するため、安全性を保つ制約があります。

- Copilot はリポジトリへの読み取りアクセスを持ち、書き込みは作業用ブランチに限られます。
- cloud agent は GitHub Actions 内で、一時的な独立環境を作成して実行されます。
- GitHub Actions ワークフローの実行には、人間の承認が必要です。
- Model Context Protocol (MCP) サーバーなど、[外部リソースへのアクセスは既定で制限されています][agent-firewall]。

## 生成されたドキュメントをレビューする

最初に、コードへドキュメントを追加するために GitHub Copilot cloud agent が作成したプルリクエスト (PR) を、GitHub.com の標準的な PR インターフェイスで確認します。

> [!NOTE]
> PR に、GitHub Copilot がファイアウォールでブロックされたという警告が表示されることがあります。既定では外部の Model Context Protocol (MCP) サーバーへの呼び出しなど、外部リソースへのアクセスが制限されているため、これは想定される動作です。必要であれば、[Copilot cloud agent のファイアウォールをカスタマイズまたは無効化][agent-firewall]できます。

1. github.com のリポジトリに戻ります。
2. **Pull Requests** を選択して PR の一覧を開きます。
3. **Add missing documentation** などのタイトルの PR を開きます。

> [!NOTE]
> Copilot がまだ作業中の場合、PR のタイトルに **[WIP]** が付きます。完了するまで待ちます。数分かかる場合があるため、休憩したり、学んだことを振り返ったりしてください。

4. 準備ができたら **Files changed** タブを選び、変更をレビューします。

   ![Files changed タブ](../../../_images/shared-pr-files-changed.png)

5. TSDoc のドキュメント コメントなど、更新されたコードを確認します。実際の変更は環境によって異なります。演習 2 で確認した指示ファイルに基づく、TSDoc、TypeScript 規約、ファイルヘッダーに注目してください。
6. 問題がなければ **Conversation** タブに戻り、下にスクロールします。
7. ワークフローが承認待ちになっていることを示す表示を探します。
8. 承認待ちのワークフローがある場合は、**Approve and run workflows** を選択します。

   ![ワークフローを承認して実行するボタン](../../../_images/shared-approve-workflows.png)

9. PR のチェック セクションにワークフローがキューイングされることを確認します。単一 Astro アプリのプロジェクト チェックが成功するまで待ちます。数分かかる場合があります。

## GitHub Copilot に変更を依頼する

PR 上のコメントで、チーム メンバーに依頼するのと同じように **@copilot** をメンションし、Copilot に変更を依頼できます。Copilot はコメントを確認し、別のセッションで対応します。結果は確率的に変わるため、決まった文面を指定することはできません。たとえば、次のような変更を依頼できます。

- 各コード ファイルの先頭に、役割を短く説明するコメントを追加する。
- TypeScript と Astro ファイルに TSDoc コメントを追加する。
- Astro アプリの構成を説明する README を作成する。

1. これらの例などを使い、生成されたドキュメントへの変更を依頼するコメントを追加し、**@copilot** をメンションします。
2. **View Session** を選択して、Copilot が作業する様子を確認します。変更用に新しいセッションが始まります。
3. **Back to pull request** を選択して PR に戻ります。

   ![プルリクエストに戻るボタン](../../../_images/ex7-back-to-pr.png)

4. Copilot の作業完了後、PR に新しいコミットがあることを確認します。
5. **Files changed** タブで変更をレビューします。

満足するまで反復できます。問題がなければ、ドラフト PR をレビュー可能な状態にして `main` ブランチにマージします。

![レビュー可能な状態に変更するボタン](../../../_images/ex7-ready-for-review.png)

## 関連ゲーム機能をレビューする

次は、ゲーム詳細ページに関連ゲームを表示する Issue に対し、Copilot が作成した PR を確認します。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選びます。
3. **Show related games on the game details page** などのタイトルの PR を選択します。
4. **Files changed** タブで生成されたコードをレビューします。
5. 問題がなければ **Conversation** タブに戻り、下にスクロールします。
6. ワークフローが承認待ちになっていることを示す表示を探します。
7. 承認待ちのワークフローがある場合は、**Approve and run workflows** を選択します。

   ![ワークフローを承認して実行するボタン](../../../_images/shared-approve-workflows.png)

8. PR のチェック セクションにワークフローがキューイングされ、単一 Astro アプリのチェックが成功することを確認します。数分かかる場合があります。
9. **任意:** Codespace でこのブランチに切り替えて、関連ゲーム機能を手動で試せます。Codespace のターミナルを開き、Copilot が作成したブランチ名 (例: **copilot/fix-8**) に置き換えて、次のコマンドを実行します。

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

関連ゲーム機能が実装されました。Copilot cloud agent に追加の変更を依頼しながら改善できます。たとえば、表示する関連ゲームの数を調整したり、カスタム指示を追加する前に割り当てたタスクにファイルヘッダーや TSDoc コメントを追加したりできます。前と同じように、**Conversation** タブでコメントを追加すると、Copilot が確認して新しいセッションを開始します。

## アクセシビリティ機能をレビューする

最後に、アクセシビリティ用カスタムエージェントで実装した機能をレビューします。この PR には、演習 3 で依頼したハイコントラスト モードと、演習 4 の Mission control で追加を依頼したライトモードの両方が含まれているはずです。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選びます。
3. **Add high contrast mode to website** などのタイトルの PR を開きます。

> [!NOTE]
> Copilot が作業中の場合、PR のタイトルに **[WIP]** が付きます。完了まで待ちます。数分かかる場合があります。

4. **Files changed** タブでコードをレビューします。
5. 実装を確認し、特に次の点を確認します。
   - モード切り替え用の UI コンポーネント
   - ユーザー設定を保存する local storage の使用
   - ハイコントラスト モードとライトモードのカスケーディング スタイル シート (CSS) またはスタイル変更
   - Accessible Rich Internet Applications (ARIA) ラベルやキーボード操作など、アクセシビリティ属性
   - モード切り替えを管理する JavaScript/TypeScript コード

6. 問題がなければ **Conversation** タブに戻り、下にスクロールします。
7. ワークフローが承認待ちになっていることを示す表示を探します。
8. 承認待ちのワークフローがある場合は、**Approve and run workflows** を選択します。

   ![ワークフローを承認して実行するボタン](../../../_images/shared-approve-workflows.png)

9. PR のチェック セクションにワークフローがキューイングされ、単一 Astro アプリのチェックが成功することを確認します。数分かかる場合があります。
10. **任意:** Codespace でブランチに切り替え、アクセシビリティ機能を手動で確認できます。Copilot が作成したブランチ名に置き換えて、次のコマンドを実行します。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    アプリを起動し、ブラウザーでハイコントラストとライトモードの切り替えを試します。ページを再読み込みしても設定が保持されることを確認します。

アクセシビリティ用カスタムエージェントが、ベスト プラクティスに沿うよう Copilot を導いたことを確認してください。アクセシビリティ上の問題や改善点があれば、ほかの PR と同様にコメントで **@copilot** をメンションして修正を依頼できます。

## オプションの演習 — 委任を続ける

cloud agent に実際のバックログ項目を任せ、その間に別の作業を進める習慣を身に付けます。リポジトリに Issue を追加し、Copilot に割り当ててみてください。

- ゲーム詳細ページに支援者向け問い合わせフォームを作成する。
- ゲーム一覧ページにページネーションを実装する。
- データアクセス ヘルパーに入力検証とエラー処理を追加する。

## まとめ

Cloud agent の環境で一連の作業を完了しました。

- このリポジトリに含まれるカスタム指示ファイルを確認し、cloud agent の出力への影響を確認しました。
- Issue を Copilot cloud agent に割り当て、環境の準備、計画、非同期の実行を確認しました。
- アクセシビリティ用カスタムエージェントを作成して使用し、ハイコントラストとライトモードの切り替えを追加しました。
- Copilot agents ページを Mission control として使い、進行中のアクセシビリティ セッションを監視して方向付けました。
- cloud agent の PR をレビューして反復し、**@copilot** に変更を依頼し、ワークフローを承認しました。

## 振り返りと次のステップ

Cloud agent の環境での作業は完了です。ほかの環境のワークショップでは、今回の練習を別の方法で続けられます。

- 🖥️ **[VS Code 環境のワークショップ](../../vscode/)** — 統合開発環境 (IDE) で Copilot Chat のエージェントモードと MCP 統合を確認します。
- 💻 **[CLI 環境のワークショップ](../../cli/)** — Plan と Autopilot、エージェント スキル、QA カスタムエージェント、Playwright MCP、Agent Merge、cloud agent への任意の `/delegate` を使い、ターミナルからレビュー済みの変更を 2 つ届けます。

自分のリポジトリでは、次の案を試してください。

- リファクタリングやテスト カバレッジの Issue を cloud agent に割り当てます。
- 別の分野向けのカスタムエージェントを作成します。
- 別の技術スタック向けに `copilot-setup-steps.yml` を設定します。

## リソース

- [GitHub Copilot][github-copilot]
- [Copilot agents について][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローのベスト プラクティス][cloud-agent-best-practices]
- [Copilot cloud agent ファイアウォールの設定][agent-firewall]

---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
