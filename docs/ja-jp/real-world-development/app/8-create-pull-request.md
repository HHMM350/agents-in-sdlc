---
title: "レッスン 8 - 機能 PR の作成とマージ"
description: "フィルター機能、指示、スキルの更新、QA プロファイル、テストをまとめてレビューし、PR を作成して Agent Merge を使用します。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

絞り込み機能の実装、指示の更新、スキルの更新、quality assurance (QA) プロファイル、テストを 1 つのブランチに保存しました。すべてまとめてレビューし、プルリクエストを作成しましょう。星評価のプルリクエスト (PR) は手動でマージしましたが、今回は **Agent Merge** にプロセスを任せます。

> [!NOTE]
> 通常は、機能、指示の更新、スキルの更新、QA エージェントを複数の PR に分けます。このワークショップでは、手順を簡潔にするため、絞り込みと品質のワークフロー全体を 1 つのセッションとブランチにまとめて PR にします。

このレッスンでは、次の作業を行います。

- Agent Merge と、マージまでのライフサイクルを自動化する方法を学びます。
- 機能 PR 全体と検証結果を調べます。
- レビュー後に Agent Merge を承認し、PR がマージされたことを確認します。

## シナリオ

絞り込みのワークフローを通して、Copilot で機能を計画、実装、検証しました。Tailspin Toys では、マージの承認を開発者の管理下に置きながら、PR の残りの作業を自動化したいと考えています。

## Agent Merge について

**Agent Merge** は、GitHub Copilot app でプルリクエストをマージするまでに必要な残りの作業を自動化します。有効にすると、アプリのセッションがプルリクエストを読み込み、失敗した継続的インテグレーション (CI) チェックの修正、レビューコメントへの対応、必要に応じたリベースなど、マージを妨げている問題に対処します。GitHub で許可され次第マージします。バックグラウンドで動作し、アプリを再起動しても継続し、プルリクエストがマージされると自動的に停止します。

ここまでは自分で **Merge pull request** を選択していました。Agent Merge に任せることもできますが、コードの編集やマージには引き続き明示的な承認が必要です。マージを許可する前に、許可される操作と作業内容をレビューしてください。

## Agent Merge で PR を管理する

コードの作成とレビューが完了したので、Agent Merge に PR の処理を任せましょう。

1. エージェントピッカーで **Default agent** を選択します。
2. **Create PR** の横にあるドロップダウンを選択します。
3. **Agent Merge** を選択します。ボタンが **Agent Merge** に変わります。
4. **Agent Merge** ボタンを選択してプロセスを開始します。ドロップダウンのオプションを選ぶだけでは開始されません。

Agent Merge が開始され、次の作業を行います。

- タイトルと説明を付けてプルリクエストを作成します。
- Issue からセッションを開始した場合は、説明本文に関連する Issue を記載します。
- ターゲットブランチへのリベースや、発生したマージ競合に対処します。
- CI を監視し、すべてのチェックが成功することを確認します。
- 他の開発者または Copilot code review からのフィードバックを監視し、コメントを解決するために更新します。
- すべて成功した後、必要に応じて PR を自動的にマージします。

すべてのチェックに成功した後、Agent Merge に PR をマージさせます。

5. マージを許可する前に、PR の差分と検証結果をレビューします。
6. **Agent Merge** の横にあるドロップダウンを選択します。
7. **Merge pull request** の横にチェックが付いていることを確認します。
8. 次のように明示して、エージェントにマージを依頼します。

    ```plaintext
    Merge the PR once all required checks and approvals pass. Do not bypass repository protections.
    ```

9. 進捗を確認し、報告された問題を解決します。続行前に、PR の状態が **Merged** になっていることを確認します。マージ権限の有効化やエージェントの実行中表示だけでは、マージ完了の確認になりません。

> [!IMPORTANT]
> Agent Merge は、リポジトリの保護や権限不足を回避しません。続行前にそれらの阻害要因を解決してください。

## まとめと次のステップ

コードの生成、テストと検証、プルリクエストの処理など、開発プロセスの一部を自動化しました。このレッスンでは、次の作業を行いました。

- Agent Merge と、マージまでのライフサイクルを自動化する方法を学びました。
- 機能 PR 全体と検証結果を調べました。
- レビュー後に Agent Merge を承認し、PR がマージされたことを確認しました。

次は[既存のキャンバスを使い、トリアージキャンバスを作成します][next-lesson]。エージェントと一緒に作業を確認、計画、視覚化するための、より豊かな方法を学びます。

## リソース

- [GitHub Copilot app での Issue とプルリクエストの管理][managing-issues-prs]
- [GitHub Copilot app について][about-copilot-app]

[next-lesson]: ../9-canvases/
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
