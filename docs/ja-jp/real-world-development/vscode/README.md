---
slug: ja-jp/real-world-development/vscode
title: "Visual Studio Code"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

VS Code の **[GitHub Copilot Chat](https://code.visualstudio.com/docs/copilot/chat/copilot-chat)** を使うと、普段使っているコードエディターで GitHub Copilot を利用できます。Visual Studio Code と GitHub Codespaces で Copilot Chat のエージェントモードを操作し、MCP サーバーを接続して、カスタムエージェントを活用します。IDE を離れずに作業でき、Copilot はファイル、ターミナル、問題をすべて把握できます。

まずカスタム指示を追加し、Copilot がその指示に従う様子を確認します。次に、エージェントモードを使って UI、データ層、テストにまたがるフィルター機能を構築します。その後、Playwright MCP サーバーを接続し、プルリクエストを作成する前に Copilot にブラウザーを操作させて機能をテストします。最後に、アクセシビリティ作業用のカスタムエージェントをレビューして使い、エージェントセッションを監視して方向付けながら、結果を反復して改善します。すべてエディターを離れずに進められます。

## 演習

| 演習 | トピック | 説明 |
|----------|-------|-------------|
| [0. 前提条件][ex0] | セットアップ | リポジトリと Codespace を作成します |
| [1. カスタム指示][ex1] | コンテキスト | VS Code でカスタム指示を追加して検証します |
| [2. エージェントモード][ex2] | コード生成 | エージェントモードでフィルター機能を構築します |
| [3. Playwright による MCP][ex3] | 外部ツール | Playwright MCP サーバーを使ってブラウザーで機能をテストします |
| [4. カスタムエージェント][ex4] | 専門エージェント | カスタムエージェントをレビューして使います |
| [5. エージェントの管理][ex5] | 監視 | エージェントセッションを監視して方向付けます |
| [6. 反復して改善する][ex6] | レビュー | PR をレビューし、Copilot の作業を反復して改善し、次のステップを選びます |
| [任意: Foundry を組み込む][foundry-toolkit] | AI エージェント | VS Code と Foundry Toolkit を使う 3 つのモジュールで、モデルを準備し、エージェントをデプロイしてサイトに接続します |

## 前提条件

このワークショップに参加する前に、次のものを用意してください。

- [ ] **Copilot Student、Pro、Pro+、Business、Enterprise** のいずれかの有効なプランがある GitHub アカウント
- [ ] GitHub Codespaces へのアクセス

> [!TIP]
> 有料プランを利用していない場合でも、認証済みの学生は [GitHub Education][callout-student-plan-education] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使うエージェント、MCP、コードレビュー、Copilot CLI の機能が含まれているため、すべてのハーネスを完了できます。

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> このハーネスでは MCP を扱いません。Copilot で MCP サーバーを使う方法については、[CLI ハーネス](../cli/)または [cloud agent ハーネス](../cloud/)を参照してください。

## はじめに

**[演習 0: 前提条件から始める →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-agent-mode/
[ex3]: 3-mcp/
[ex4]: 4-custom-agents/
[ex5]: 5-managing-agents/
[ex6]: 6-iterating/
[foundry-toolkit]: 7-foundry-toolkit/
