---
slug: ja-jp/real-world-development/cli
title: "GitHub Copilot CLI"
authors:
  - geektrainer
description: "Copilot CLI のモード、カスタマイズ、MCP ツール、プルリクエストの自動化を学びながら、Tailspin Toys の変更を構築、検証、公開します。"
lastUpdated: 2026-09-18
---

**[GitHub Copilot CLI][about-copilot-cli]** は、ターミナルで GitHub Copilot をエージェント型のコーディングアシスタントとして利用できるようにします。コードベースを探索し、コードを生成し、コマンドを実行し、外部ツールに接続できます。すべてコマンドラインから行えるため、グラフィカルエディターに切り替えずに作業の流れを保てます。

このワークショップでは、Tailspin Toys の一連の開発ワークフローに沿って作業します。

1. GitHub Codespaces でプロジェクトを準備し、Copilot CLI をインストールして概要を確認します。
2. 星評価の変更を行い、ブラウザーでレビューして、最初のプルリクエスト (PR) を手動でマージします。
3. 絞り込み Issue から始め、Plan モードで方針を決め、Autopilot モードで実装し、Interactive モードでレビューします。
4. リポジトリの指示を更新し、絞り込み機能の作業に適用します。
5. 既存の `quality-checks` スキルをカスタマイズして、プロジェクトのチェックを実行します。
6. Playwright Model Context Protocol (MCP) サーバーを追加し、ブラウザーで絞り込み機能を確認します。
7. 品質保証 (QA) カスタムエージェントを作成し、要件、テストカバレッジ、検証結果をレビューします。
8. 絞り込み機能全体をレビューし、Agent Merge を使って PR を処理します。
9. コンテキスト、モデル、共有、クラウドエージェントへの任意の委任に役立つスラッシュコマンドを確認します。

ワークショップで作成する PR は 2 つです。1 つ目は星評価、2 つ目は絞り込み機能と指示・スキル・QA プロファイル・テストの更新です。絞り込みと品質のワークフローでは、1 つの会話とブランチを引き続き使うため、各ツールを学びながらこれまでの作業を活用できます。

## 演習

| 演習 | トピック | 説明 |
|----------|-------|-------------|
| [0. 前提条件][ex0] | セットアップ | リポジトリと codespace を作成する |
| [1. Copilot CLI のインストール][ex1] | インストール | Copilot CLI をインストールして認証し、基本を確認します |
| [2. 星評価を追加する: 小さな改善][ex2] | 最初の変更 | 既存の評価と評価がない場合の表示を追加し、最初の PR をマージします |
| [3. エージェントモード: Plan と Autopilot][ex3] | エージェントモード | Issue から機能を計画し、Autopilot で構築して Interactive モードでレビューします |
| [4. カスタム指示で Copilot を導く][ex4] | コンテキスト | 指示を確認、更新し、絞り込み機能に適用します |
| [5. quality-checks スキルのカスタマイズと使用][ex5] | 繰り返し実行できるチェック | 既存スキルを確認し、レポート形式を変更して実行します |
| [6. Playwright MCP で機能を検証する][ex6] | ブラウザーでの確認 | CLI で MCP を設定し、絞り込みの動作を確認します |
| [7. QA エージェントの作成と使用][ex7] | 要件とカバレッジ | 専門プロファイルを作成して選択し、検証結果を集めます |
| [8. 機能 PR の作成とマージ][ex8] | レビューとマージ | 変更全体をレビューし、PR を作成して Agent Merge を使用します |
| [9. GitHub Copilot CLI のスラッシュコマンド][ex9] | CLI 機能 | コンテキスト、モデル、共有、クラウドエージェントへの任意の委任を確認します |
| [10. 振り返りと次のステップ][ex10] | まとめ | ワークフロー、再利用可能なカスタマイズ、追加リソースを確認します |
| [オプション: Foundry を組み込む][foundry] | ホスト型エージェント | モデルを準備し、カタログに基づいた Backer Concierge を構築してデプロイし、Web サイトに接続する |

## 前提条件

このワークショップに参加する前に、次のものを用意してください。

- [ ] **Copilot Student、Pro、Pro+、Business、Enterprise** のいずれかの有効なプランがある GitHub アカウント
- [ ] リポジトリと Codespace を作成する権限
- [ ] ターミナルまたはコマンドライン操作の基本的な知識

> [!TIP]
> 有料プランを利用していない場合、認証済みの学生は [GitHub Education][callout-student-plan-education] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使用するエージェント、MCP、コードレビュー、Copilot CLI の機能が含まれています。

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> Copilot Business または Copilot Enterprise を使用している場合は、管理者が Copilot CLI を有効にしていることを確認してください。

## はじめる

**[演習 0: 前提条件から始める →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-cli/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-cli-power-tools/
[foundry]: 8-foundry-agent/
[ex10]: 10-review/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
