---
slug: ja-jp/real-world-development/app
title: "GitHub Copilot app"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

[**GitHub Copilot app**](https://docs.github.com/copilot/concepts/agents/github-copilot-app) は Copilot CLI を基盤とするデスクトップアプリケーションで、エージェント主導の開発を単一の作業環境で実現します。複数のエージェントセッションを並行して実行し、セッションモードを切り替え、キャンバスで共同作業し、GitHub Issue とプルリクエストをネイティブに管理できます。さらに **Agent Merge** を使うと、プルリクエストのリベース、レビューのフィードバック、継続的インテグレーション (CI) の修正、マージまでを一貫して進められます。

このワークショップでは、Tailspin Toys で一連の作業を行います。

1. プロジェクトを準備し、アプリをインストールしてリポジトリを接続し、ワークスペースと用意されたバックログを確認します。
2. 星評価の変更を行い、ブラウザーでレビューして、最初のプルリクエスト (PR) を手動でマージします。
3. 絞り込みの Issue から始め、**Plan** モードで方針を決め、**Autopilot** モードで実装し、**Interactive** モードでレビューします。
4. リポジトリの指示を更新し、絞り込みの作業に適用します。
5. 既存の `quality-checks` スキルをカスタマイズして、プロジェクトのチェックを実行します。
6. Playwright Model Context Protocol (MCP) サーバーを追加し、ブラウザーで絞り込みの動作を確認します。
7. quality assurance (QA) カスタムエージェントを作成し、要件、カバレッジ、検証結果をレビューします。
8. 絞り込みの変更全体をレビューし、2 件目の PR に Agent Merge を使用します。
9. キャンバスが利用可能か確認し、Database Explorer を使ってから、リポジトリに保存するトリアージキャンバスを作成してテストします。必要な機能を利用できない場合は、ブロッカーを記録し、読み取り専用の代替手段を使うか、まとめに進みます。

ワークショップでは、星評価と、指示の更新、スキルの更新、QA プロファイル、テストを含む絞り込み機能の 2 件の PR を作成します。どちらも更新済みの `main` から開始します。絞り込みと品質のワークフローでは、1 つのセッション、worktree、ブランチを使います。最後のキャンバス演習も同じセッションで行い、PR の手順を繰り返さずに共有サーフェスの作成とテストに集中します。

## レッスン

| レッスン | トピック | 説明 |
|--------|-------|-------------|
| [0. 前提条件][ex0] | セットアップ | Node.js をインストールし、Tailspin Toys プロジェクトの自分用コピーを作成します |
| [1. Copilot app のインストール][ex1] | セットアップ | アプリをインストールしてプロジェクトを接続し、ワークスペースを確認します |
| [2. 星評価の追加: すぐできる改善][ex2] | 最初の変更 | 既存の評価と null の場合の表示を追加し、最初の PR をマージします |
| [3. エージェントモード: Plan と Autopilot][ex3] | エージェントモード | Issue から機能を計画し、Autopilot で構築して、Interactive モードでレビューします |
| [4. カスタム指示で Copilot をガイドする][ex4] | コンテキスト | 指示を確認・更新し、絞り込み機能に適用します |
| [5. quality-checks スキルをカスタマイズして使う][ex5] | 繰り返し可能なチェック | 既存のスキルを確認し、レポート形式を変更して実行します |
| [6. Playwright MCP で機能を検証する][ex6] | ブラウザーでの確認 | Customize で MCP を設定し、絞り込みの動作を調べます |
| [7. QA エージェントを作成して使う][ex7] | 要件とカバレッジ | 専門家プロファイルを作成して選択し、最終検証の結果を集めます |
| [8. 機能の PR を作成してマージする][ex8] | レビューとマージ | 変更全体をレビューして 2 件目の PR を作成し、Agent Merge を使います |
| [9. キャンバスを確認して作成する][ex9] | コラボレーション | Database Explorer を使用してから、リポジトリに保存するトリアージキャンバスを作成してテストします。機能を利用できない場合は、ブロッカーを記録して代替手段を使うか、まとめに進みます |
| [10. まとめと次のステップ][ex10] | まとめ | ワークフロー、再利用できるカスタマイズ、その他のリソースを確認します |

## 前提条件

このワークショップに参加する前に、次のものを用意してください。

- [ ] **Copilot Student、Pro、Pro+、Business、Enterprise** のいずれかの有効なプランがある GitHub アカウント
- [ ] **macOS、Linux、Windows** のいずれかを実行するコンピューター
- [ ] コンピューターに[インストールされた Git][install-git]

> [!TIP]
> 有料プランを利用していない場合でも、認証済みの学生は [GitHub Education][callout-student-plan-education] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使うエージェント、MCP、コードレビュー、Copilot CLI の機能が含まれているため、すべてのハーネスを完了できます。

> [!NOTE]
> Copilot app は Codespace ではなく自分のコンピューターで実行します。[レッスン 0][ex0] ではアプリをインストールする前に Node.js をインストールし、プロジェクトの自分用コピーを作成します。

> [!NOTE]
> Copilot Business または Copilot Enterprise を使用している場合、アプリを利用するには管理者が **GitHub Copilot app** ポリシーを有効にしておく必要があります。これは Copilot CLI のポリシーとは別の設定です。

## はじめに

**[レッスン 0「前提条件」から始める →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-app/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-canvases/
[ex10]: 10-review/
[install-git]: https://github.com/git-guides/install-git
[callout-student-plan-education]: https://github.com/education/students
