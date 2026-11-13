---
title: "レッスン 2 - 星評価の追加: すぐできる改善"
description: "Copilot CLI でゲームカードに小さな変更を加え、転送ブラウザーで確認して、最初のプルリクエストとしてマージします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Copilot CLI をインストールし、会話を試したので、プロジェクトに最初の変更を加えましょう。今回は小さな変更です。ゲームデータには星評価がありますが、ホームページのゲームカードにはまだ表示されていません。エージェントに評価を表示させ、変更をレビューし、最初のプルリクエストとしてマージします。

このレッスンでは、次の作業を行います。

- 機能ブランチで目的を絞った Copilot の会話を開始します。
- エージェントに小さな変更を依頼します。
- `/diff` で変更をレビューします。
- 転送ブラウザーでアプリを実行し、変更を確認します。
- 最初のプルリクエストを作成してマージします。

## シナリオ

Tailspin Toys の各ゲームには星評価を設定でき、ゲーム詳細ページにはすでに表示されています。しかし、ホームページのゲームカードに表示されるのはタイトル、カテゴリ、パブリッシャー、説明だけです。最初の練習として、各カードに既存の評価を表示するようエージェントに依頼します。小さく完結した変更なので、最初のセッションに最適です。

## 会話の構成

**会話**では、Copilot CLI と一緒にタスクに取り組みます。Copilot app とは異なり、通常の CLI 会話では専用の worktree を作らず、ターミナルで現在チェックアウトしているリポジトリと Git ブランチを使います。保存した会話に戻って同じやり取りを続けられます。ファイルとブランチは通常の Git 状態としてディスク上に残ります。

会話では、プロンプトとエージェントの応答、ファイルを調査・編集するエージェントの操作、`/diff` で調べられる変更を確認できます。

## 会話を開始して変更を依頼する

新しい会話を開始して、機能を実装しましょう。

1. Codespace に戻ります。
2. ターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
3. まだ Copilot を起動していない場合は、次のコマンドを実行します。

   ```bash
   copilot --yolo
   ```

4. スラッシュコマンド `/new` を入力し、<kbd>Enter</kbd> を押して新しいセッションを開始します。
5. 次のプロンプトで変更を依頼します。

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot はプロジェクトを調べ、ゲーム詳細の表示に使われているファイルを見つけて、必要なコードを作成します。Copilot CLI を使って新しい機能を追加できました。

## 差分をレビューする

小さな変更であっても、マージする前に AI が生成した変更をレビューしてください。Copilot CLI で変更を確認します。

1. `/diff` を入力して、変更されたファイルをすべて確認します。
2. ゲームカードに評価がある場合は数値が、`starRating` が `null` の場合は `No rating yet` が表示されることを確認します。
3. テストで両方の状態が検証されていることを確認します。
4. Copilot が実行したチェックの結果を確認し、失敗があれば修正を依頼します。
5. レビューが終わったら <kbd>Esc</kbd> を押して差分画面を閉じます。

> [!NOTE]
> すべての生成 AI ツールと同様に、Copilot の動作は確率的であり、決定論的ではありません。コードは例と異なる場合があります。特定の実装に固執せず、動作を確認してください。

## 変更を確認する

コードを読むだけで動作すると判断するのではなく、Copilot に Web サイトを起動させ、Codespaces が転送したブラウザーで更新された UI を確認します。

1. Copilot にアプリの起動を依頼します。

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces でポート `4321` が利用可能になったら **Open in Browser** を選択します。
3. ゲームカードに 5 段階評価が表示されることを確認します。
4. Copilot に戻り、起動したサーバーを停止するよう依頼します。

   ```plaintext
   Stop the development server you started.
   ```

## 最初のプルリクエストを作成してマージする

機能を作成できました。コードをプロジェクトにマージするため、プルリクエスト (PR) を作成します。

1. 既定のエージェントに変更をコミットするよう依頼します。

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. `/pr create` を入力します。Copilot CLI は PR の作成時に既存のコミットをプッシュし、PR の URL を表示します。
3. Copilot CLI が表示した URL を、<kbd>Command</kbd> (Mac) または <kbd>Ctrl</kbd> (Windows/Linux) を押しながら選択して PR を開きます。
4. 変更されたファイルとチェックをレビューします。
5. 準備ができたら **Merge pull request** を選択し、マージを確認します。
6. Codespace に戻り、`/exit` で Copilot CLI を終了します。
7. ローカルの `main` を更新します。

   ```bash
   git checkout main
   git pull
   ```

## まとめと次のステップ

GitHub Copilot CLI を使って最初の変更をリリースできました。このレッスンでは、次の作業を行いました。

- 機能ブランチで目的を絞った Copilot の会話を開始しました。
- エージェントにゲームカードの小さな変更を依頼しました。
- `/diff` で変更をレビューしました。
- 転送ブラウザーでアプリを実行し、星評価を確認しました。
- 最初のプルリクエストを作成してマージしました。

次は[絞り込みの Issue から始め、Plan と Autopilot モードを使って][next-lesson]、より大きな機能を作成します。

## リソース

- [GitHub Copilot CLI について][about-copilot-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
