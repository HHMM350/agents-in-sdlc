---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

ここまでの演習では、ユーザー体験の改善や機能の追加を目的とした 3 つのタスクを Copilot cloud agent に依頼しました。cloud agent は非同期かつ自律的に作業しますが、タスクを監視することも重要です。

cloud agent に割り当てたタスクを管理するツールはいくつかあります。GitHub.com の[エージェントページ][agents-page]もその 1 つです。この Mission control では、オープンなプルリクエスト (PR) があるすべてのエージェントタスクを確認できます。実行内容を調べたり、進行中のセッションに追加の指示を送ったりできます。

このレッスンでは、次の作業を行います。

- エージェントページで cloud agent のタスクを監視します。
- 進行中のセッションに機能追加を依頼します。

## シナリオ

ハイコントラストモードの作成をエージェントに割り当てた後、チームはライトモードも追加するよい機会だと考えました。すでにサイトのスタイルを更新し、切り替え機能を追加しているため、一緒に実装するのが妥当です。ハイコントラストに加えてライトモードも追加されるよう、エージェントの作業を方向付けます。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てたタスクの現在の状態を確認しましょう。

1. [Copilot agents ページ](https://github.com/copilot/agents)に移動します。
2. メインパネルと左側のパネルにあるタスク一覧を確認します。次のようなタスクが表示されます。
   - コードのドキュメントを更新する。
   - ゲーム変更用の API を生成する。
   - Web サイトにハイコントラストモードを追加する。
3. 実行中のタスクを選択し、Copilot が行った作業を確認します。リポジトリからのコードのチェックアウト、作業環境や MCP サーバーの準備、タスク完了に向けたさまざまな処理を確認できます。

> [!NOTE]
> 表示される手順は Copilot の作業状況や実行方法によって異なります。

4. 右側の PR パネルも確認します。ここから PR と変更されたファイルを確認し、進行状況を監視できます。

## Cloud agent に指示を追加する

実行中のタスクを確認したので、エージェントがハイコントラストモードを作成している間に、ライトモードの切り替えも追加するよう依頼します。

1. ハイコントラストモードの作成を依頼したセッションを選択します。エージェントが付けた名前や作業状況によって、タイトルは異なります。

    ![Mission control のアクセシビリティセッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが完了して作業が始まるまで、数分間セッションを確認します。Copilot の進行状況が更新され始めたら作業開始を確認できます。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを入力します。

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![エージェントページで作業中の cloud agent に指示するダイアログを強調表示した画面](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot がプロンプトを受け取り、作業手順に追加したことを確認します。

## Copilot に作業を任せる

Copilot は更新されたタスクに取り組みます。メッセージを送信した時点で作業していた手順が終わると、新しい依頼をワークフローに組み込みます。

今回も完了まで数分かかります。その間に、ここまでに学び、確認した内容を振り返りましょう。

## まとめと次のステップ

GitHub Copilot cloud agent の監視とガイダンスの中心となる、Copilot agents ページを学びました。この Mission control では、進行中または完了したすべてのタスクを追跡し、実行中の作業をレビューし、進行中のタスクの範囲を変更したり追加のガイダンスを提供したりできます。

次の内容を学びました。

- Mission control とエージェントページで cloud agent のタスクを監視する方法。
- 進行中のセッションに追加機能を依頼する方法。

Copilot がアクセシビリティ機能を実装している間に、次は Copilot が作成したプルリクエストを[反復して改善します][next-lesson]。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタムエージェントについて][custom-agents]

---

| [← 前のレッスン: カスタムエージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復して改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
