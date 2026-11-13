---
title: "レッスン 8 - 機能 PR の作成とマージ"
description: "絞り込み機能、指示、スキルの更新、QA プロファイル、テストをまとめてレビューし、PR を作成して Agent Merge を使用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

絞り込み機能、指示の更新、スキルの更新、quality assurance (QA) プロファイル、テストを 1 つのブランチに保存しました。すべてまとめてレビューしてプルリクエストを作成しましょう。星評価のプルリクエスト (PR) は手動でマージしましたが、今回は **Agent Merge** にマージの作業を任せます。

> [!NOTE]
> 通常は機能、指示の更新、スキルの更新、QA エージェントを複数の PR に分けます。このワークショップでは、手順を簡潔にするため、絞り込みと品質のワークフロー全体を 1 つの会話とブランチにまとめて PR にします。

このレッスンでは、次の作業を行います。

- Agent Merge と、マージまでのライフサイクルを自動化する方法を学びます。
- 機能の変更全体と検証結果を調べます。
- 絞り込みの PR を作成します。
- レビュー後にのみ Agent Merge を有効にして、PR がマージされたことを確認します。

## シナリオ

絞り込み機能のワークフローを通して、Copilot で機能を計画、実装、検証しました。Tailspin Toys では、マージの最終承認を開発者が管理しながら、PR の残りの作業を自動化したいと考えています。

## Agent Merge について

**Agent Merge** はプルリクエストをマージするために必要な残りの作業を自動化します。有効にすると、Copilot は PR を妨げている問題を解決します。たとえば、失敗した継続的インテグレーション (CI) チェックの修正、レビューコメントへの対応、必要に応じたリベースを行います。その後、リポジトリで許可されていれば GitHub の自動マージを有効にします。

ここまでは自分で **Merge pull request** を選択していました。Agent Merge にその作業を任せられます。有効にする前に、作業をレビューして準備ができていることを確認してください。

## Agent Merge で PR を管理する

コードの作成が終わったら、全体をレビューして PR を作成し、残りの作業を Agent Merge に任せましょう。

1. Codespace に戻ります。
2. `/agent` を入力してエージェントのダイアログを開きます。
3. 一覧から **Default** を選択し、<kbd>Enter</kbd> を押します。
4. `/pr create` コマンドで新しい PR を作成します。
5. `/pr agentmerge` を使って Agent Merge を有効にします。
6. Copilot が PR の継続的インテグレーションを監視します。すべて成功すると、マージを実行します。
7. Copilot から「PR #14 was squash-merged successfully.」のようなメッセージが届いたことを確認します。

> [!IMPORTANT]
> Agent Merge は、必須の承認、ブランチ保護、マージキュー、リポジトリ設定、権限の不足を回避しません。作業がブロックされた場合は報告された理由を確認し、リポジトリで許可されている場合はレビュー済みの変更を手動でマージします。

## まとめと次のステップ

コードの生成、テスト、検証、プルリクエストの処理など、開発プロセスの一部を自動化しました。このレッスンでは、次の作業を行いました。

- Agent Merge と、マージまでのライフサイクルを自動化する方法を学びました。
- 機能の変更全体と検証結果を調べました。
- 絞り込みの PR を作成しました。
- レビュー後にのみ Agent Merge を有効にし、PR がマージされたことを確認しました。

次は、コンテキスト、モデル、共有、任意のクラウド委任に使える [Copilot CLI のスラッシュコマンド][next-lesson]を確認します。

## リソース

- [Copilot CLI でプルリクエストを管理する][manage-prs]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
