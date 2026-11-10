---
title: "演習 0: 前提条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

VS Code の演習を始める前に、必要な環境を準備します。Tailspin Toys リポジトリの自分用コピーを作成し、作業用の [codespace][codespaces] を起動して、エディターで GitHub Copilot Chat を使えることを確認します。

## 演習用リポジトリをセットアップする

コードを作成するためのリポジトリのコピーを、[テンプレート][template-repository]から作成します。このコピーには演習に必要なファイルが含まれます。以降の演習では、このリポジトリを使います。

1. 新しいブラウザーウィンドウで [Tailspin Toys テンプレート][tailspin-template]を開きます。
2. 演習用リポジトリのページで **Use this template** を選択し、続けて **Create a new repository** を選択して、自分用のコピーを作成します。

   ![Use this template ボタン](../../../_images/ex0-use-template.png)

3. GitHub または Microsoft が主催するイベントでワークショップに参加している場合は、メンターの案内に従います。それ以外の場合は、GitHub Copilot を利用できる組織に新しいリポジトリを作成します。

   ![リポジトリのテンプレート設定を入力する画面](../../../_images/ex0-repository-settings.png)

4. 作成したリポジトリのパス (**organization-or-user-name/repository-name**) を控えておきます。演習中にこのパスを使います。

> [!NOTE]
> **バックログは準備済みです**
>
> テンプレートからリポジトリを作成すると、GitHub Issue のバックログも自動的に作成されます。ワークショップではこの Issue を使うため、自分で Issue を作成する必要はありません。

## codespace を作成する

次に、演習で使う codespace を作成します。

[GitHub Codespaces][codespaces] は、ブラウザー上で直接コードの作成、実行、デバッグができるクラウド開発環境です。複数のプログラミング言語、拡張機能、ツールに対応した、機能豊富な統合開発環境 (IDE) を提供します。

1. 作成したリポジトリを開きます。
2. 緑色の **Code** ボタンを選択します。

   ![Code ボタンを選択する画面](../../../_images/ex0-code-button.png)

3. **Codespaces** タブを選択し、**+** ボタンを選択して、新しい codespace を作成します。

   ![新しい codespace を作成する画面](../../../_images/ex0-create-codespace.png)

codespace の作成には数分かかりますが、必要なサービスを手作業でインストールするよりも早く準備できます。その間に GitHub Copilot の機能を確認しておくと、次の演習に備えられます。

> [!CAUTION]
> 今後の演習でこの codespace に戻ります。
>
> 1. ひとまず、ブラウザーのタブを閉じずに開いたままにしてください。

> [!NOTE]
> このワークショップは codespace またはローカルの [開発コンテナー][dev-containers]で実行できます。どちらも、必要な前提条件が整った環境を提供します。ローカルで実行する場合は、次の手順で codespace と同じ開発コンテナーを使います。
>
> 1. クローンしたリポジトリを VS Code で開きます。
> 2. プロンプトが表示されたら **Reopen in Container** を選択します。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## GitHub Copilot Chat とエージェントモードを使う

GitHub Copilot Chat のエージェントモードを使うには、IDE に GitHub Copilot Chat 拡張機能がインストールされている必要があります。GitHub Codespace を使っている場合は、通常すでにインストールされています。

> [!TIP]
> GitHub Copilot Chat 拡張機能がインストールされていない場合は、次のいずれかの方法でインストールします。
>
> 1. [Visual Studio Code Marketplace からインストール][copilot-chat-extension]します。
> 2. Visual Studio Code の **Extensions** ビューを開き、**GitHub Copilot Chat** を検索して **Install** を選択します。

拡張機能をインストールした後、GitHub アカウントでの認証が必要になる場合があります。

1. codespace に戻ります。
2. エディターの右側に Copilot Chat が表示されていない場合は、codespace の上部にある **Copilot Chat** アイコンを選択します。
3. Copilot Chat ウィンドウに「Hello world」のようなメッセージを入力し、<kbd>Enter</kbd> キーを押します。これで Copilot Chat が起動します。
4. 認証されていない場合は、GitHub アカウントへのサインインが求められます。画面の案内に従って認証します。

   ![Copilot Chat の認証プロンプトの例](../../../_images/ex1-copilot-authentication.png)

5. 認証後、Copilot Chat ウィンドウが表示されていることを確認します。

## まとめ

演習用リポジトリのコピーを作成し、コードを書くときに使う codespace の作成を開始しました。

## 次のステップ

次は Copilot を使ってみましょう。[演習 1 - カスタム指示][next-lesson]に進み、Copilot にプロジェクトの規約を伝えます。

## リソース

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces を使い始める][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
