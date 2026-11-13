---
title: "レッスン 2 - 星評価の追加: すぐできる改善"
description: "GitHub Copilot app で最初のエージェントセッションを開始し、ゲームカードに小さな変更を加えて、最初のプルリクエストとしてマージします。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

前のレッスンでは、ワークスペースを確認し、クイックチャットを試しました。次は**エージェントセッション**を開始し、プロジェクトに最初の変更を加えます。変更は小さなものにします。ゲームのデータにはすでに星評価がありますが、ホームページのゲームカードにはまだ表示されていません。エージェントに表示を依頼し、変更をレビューして、最初のプルリクエストとしてマージします。

このレッスンでは、次の作業を行います。

- エージェントセッションを開始し、セッションの構成を学びます。
- エージェントに小規模で対象を絞った変更を依頼します。
- ワークスペースの差分ビューで変更をレビューします。
- アプリをローカルで実行し、ブラウザーで変更を確認します。
- 最初のプルリクエストを作成してマージします。

## シナリオ

Tailspin Toys の各ゲームには星評価を設定でき、ゲーム詳細ページにはすでに表示されています。しかし、ホームページのゲームカードに表示されるのはタイトル、カテゴリ、パブリッシャー、説明だけです。最初の練習として、各カードに既存の評価を表示するようエージェントに依頼します。小さく完結した変更なので、最初のセッションに最適です。

## セッションの構成

**セッション**とは、分離された独自のワークスペースで実行されるエージェントとの会話です。各セッションには**専用の git worktree とブランチ**が割り当てられます。そのため、一方で機能を追加し、もう一方でバグを修正するなど、変更を競合させずに複数のセッションを同時に実行できます。セッションはリポジトリごとにサイドバーにグループ化され、選択すると切り替えられます。

セッション内では、エージェントとの**会話**、ファイルを調査・編集するときのエージェントの**ツールアクティビティ**、差分付きの**変更済みファイル**一覧を確認できます。

## セッションを開始して変更を依頼する

新しいセッションを開始して、プロジェクトを調査し機能を実装します。[アプリのセットアップ][prior-lesson]で、GitHub リポジトリからプロジェクトを追加しました。そのリポジトリ用の新しいセッションを作成して、変更を依頼しましょう。

1. GitHub Copilot app に戻ります。アプリを閉じている場合は開きます。
2. サイドバーの上部にある **+** を選択してセッションを開始します。
3. リポジトリとして `tailspin-toys` を選択します。
4. プロンプトボックスの下で **new working tree** と **Interactive** モードを選択し、次のプロンプトを送信します。

    ```plaintext
    Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
    ```

5. <kbd>Enter</kbd> を押してプロンプトを Copilot に送信します。

Copilot app は、最初にプロジェクトの分離されたコピーである新しい worktree を作成して作業を始めます。次にプロジェクトを調査し、新機能の追加に必要なファイルを見つけ、コードを作成します。Copilot app を使って新機能を追加できました。

## 差分をレビューする

小さな変更であっても、AI が生成した変更はマージ前にレビューしてください。Copilot app で変更を確認します。

1. アプリの右上隅にある **Toggle review panel** を選択します。開いたパネルで **Changes** を選ぶと、変更されたファイルと差分が表示されます。

    ![Create PR の右側にある Toggle review panel ボタンを矢印で示した GitHub Copilot app の上部ツールバー](../../../_images/app-2-review-panel.png)

2. ゲームの詳細を表示する主要ファイル `GameCard.astro` に、評価がある場合に表示し、`starRating` が `null` の場合は "No rating yet" に切り替えるコードが追加されていることを確認します。次のようなコードです。

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> Copilot は、すべての生成 AI ツールと同様に確率的に動作するため、実際のコードは上記と異なる場合があります。比較的よく似た結果になります。

## 変更を確認する

ブラウザーを開く前に、エージェントが実行した自動チェックの結果をレビューします。数値の `starRating` と、`null` の場合の代替表示をテストしていることを確認します。前提条件が不足していたり、チェックがスキップされていたりする場合は成功ではありません。インストールの要求は内容を確認してから承認してください。

コードを読むだけで動くと判断せず、Copilot に Web サイトを起動させ、更新された UI を確認しましょう。Web サイトを起動し、ブラウザーキャンバスで開くよう依頼します。

> [!TIP]
> キャンバスは、Copilot app 内で利用できるインタラクティブなウィジェットです。後のレッスンではカスタムキャンバスを調べ、自分でも作成します。ここでは組み込みのブラウザーキャンバスを使用します。

1. 次のプロンプトで、アプリを起動してブラウザーキャンバスで開くよう Copilot に依頼します。

    ```plaintext
    Start the app and open it in the browser canvas.
    ```

2. しばらくするとアプリが起動し、Copilot app 内にブラウザーウィンドウが開きます。
3. 評価済みのゲームカードに、5 点満点の評価が表示されることを確認します。
4. 確認が終わったら、次のプロンプトでこのセッションが起動した開発サーバーを停止するよう Copilot に依頼します。

    ```plaintext
    Stop the dev server and close the browser canvas.
    ```

## 最初のプルリクエストを作成してマージする

機能を作成できました。新しいコードを既存のコードベースにマージするため、プルリクエスト (PR) を作成します。

1. 右上隅にある **Create PR** を選択します。
2. 求められた場合は **Sign in with your browser** を選択し、画面の指示に従って認証します。
3. リポジトリのポリシーにより、PR を作成する前に該当する Issue が必要だと Copilot が説明した場合は、その手順に従うよう確認します。
4. Copilot が PR を作成します。
5. チャットのすぐ上にある **PR** バブルを選択し、レビューペインで PR を開きます。必要に応じて内容をレビューします。
6. 準備ができたら **Ready to merge** を選択します。
7. 新しいダイアログで **Merge pull request** を選択し、PR をマージします。

## まとめと次のステップ

GitHub Copilot app を使って最初の変更をリリースしました。このレッスンでは、次の作業を行いました。

- エージェントセッションを開始し、セッションの構成を学びました。
- ゲームカードに小規模で対象を絞った変更を加えるようエージェントに依頼しました。
- ワークスペースの差分ビューで変更をレビューしました。
- アプリをローカルで実行し、ブラウザーで星評価を確認しました。
- PR 1 を作成し、チェックをレビューして、明示的にマージしました。

次は[絞り込みの Issue から始めて Plan と Autopilot モードを使い][next-lesson]、より大きな機能を構築します。

## リソース

- [GitHub Copilot app でのエージェントセッションの操作][agent-sessions]
- [GitHub Copilot app について][about-copilot-app]
- [GitHub Copilot app での Issue とプルリクエストの管理][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#github-copilot-app-をインストールして構成する
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
