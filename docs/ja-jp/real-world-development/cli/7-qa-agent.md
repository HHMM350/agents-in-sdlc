---
title: "レッスン 7 - QA エージェントの作成と使用"
description: "Issue の要件、quality-checks スキル、Playwright MCP を組み合わせる QA カスタムエージェントを作成します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

`quality-checks` スキルで自動チェックを実行し、Playwright MCP でブラウザーから絞り込み機能を確認しました。今度は、明確に定義した QA プロセスを持つカスタムエージェントに、これらの機能をまとめます。

このレッスンでは、次の作業を行います。

- カスタムエージェントが指示、スキル、MCP ツールと連携する方法を確認します。
- 再利用可能な品質保証プロファイルを作成して調べます。
- QA エージェントを選択し、絞り込みの Issue に照らし合わせて結果をレビューします。

## シナリオ

Tailspin Toys では、プルリクエスト (PR) を作成する前に、要件、コード品質、自動チェック、テスト範囲、ブラウザーの動作を一貫した方法でレビューしたいと考えています。カスタムエージェントを使うと、QA プロセスを調整し、再利用可能なレポートを作成できます。

## カスタムエージェントとは

カスタムエージェントは、Markdown プロファイルで定義する、Copilot の専門的な設定です。プロファイルにはエージェントの目的、指示、利用可能なツールを記載します。このワークショップでは `.github/agents/qa.agent.md` に QA の役割を定義し、Copilot CLI で選択します。

ここまでに使用したカスタマイズには、それぞれ異なる役割があります。リポジトリの指示はチームの標準を説明します。`quality-checks` スキルは繰り返し実行できるチェックをまとめます。Playwright MCP はブラウザーツールを提供します。QA プロファイルは、要件を評価して結果を報告するための機能の使い方を Copilot に伝えます。これらの置き換えや、別の会話の開始は必要ありません。

## QA プロファイルを作成する

機能 PR を作成する前に、再利用可能な QA プロファイルを Copilot に作成させます。プロファイルには、QA が実施するチェックと、その作業の制約を定義します。

1. Codespace に戻り、絞り込みの会話が Interactive モードであることを確認します。
2. 既定のエージェントに、カスタムエージェントを作成するよう依頼します。

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## プロファイルを確認する

新しいエージェントを使う前に、Copilot が意図した QA ワークフローと制約を取り込んだことを確認します。こうすることで、検証だけを行う予定なのに、不完全な指示や広すぎる権限によって機能が変更されることを防げます。

1. `/diff` を入力して `.github/agents/qa.agent.md` を開きます。
2. frontmatter を確認します。`description` は必須です。`name` は省略できますが、設定するとエージェント名がわかりやすくなります。
3. プロファイルの指示を読み、要件から作業を開始し、リポジトリの指示に従い、`quality-checks` スキルと Playwright MCP を使うことを確認します。
4. QA が根拠を示し、実装コードを変更する前に許可を求め、変更をコミットしたりプルリクエストを開いたりしないことを確認します。
5. これらの役割や制約が欠けている場合は、続行する前に既定のエージェントにプロファイルの修正を依頼します。

## Issue に対して QA を実行する

Copilot CLI は会話の開始時にプロジェクトのエージェントを読み込みます。プロファイルを作成した後、同じ絞り込みの会話を再開し、QA を選択します。そうすると、すでにコンテキストに含まれる Issue と計画の決定を利用できます。

1. 次のプロンプトでエージェントを有効にします。

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> エージェントを作成した直後は、利用可能なエージェントの一覧に表示されない場合があります。上記のコマンドを実行すると有効になります。

2. 次のプロンプトで QA エージェントに機能をレビューするよう依頼します。

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA エージェントが作業を開始します。
4. 完了したら、エージェントのレポートを確認します。

## まとめと次のステップ

再利用可能な専門的な役割をワークフローに加え、結果をレビューしました。このレッスンでは、次の作業を行いました。

- カスタムエージェントが指示、スキル、MCP ツールと連携する方法を学びました。
- 再利用可能な品質保証プロファイルを作成して調べました。
- QA エージェントを選択し、絞り込みの Issue に照らし合わせて結果をレビューしました。

実装、スキルの更新、QA プロファイル、テスト、検証レポートがそろいました。次は[機能 PR を作成して Agent Merge を使います][next-lesson]。

## リソース

- [Copilot CLI 向けカスタムエージェントの作成][create-agents]
- [カスタムエージェントの設定][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
