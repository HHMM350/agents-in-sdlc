---
title: "レッスン 3 - エージェントモード: Plan と Autopilot"
description: "Plan で実装方針を合意し、Autopilot で Issue の絞り込み機能を構築して、Interactive モードで結果をレビューします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

最初に小さな機能をプロジェクトに追加しました。より大きな変更には、もっとしっかりしたプロセスが必要です。GitHub Copilot CLI は組織の既存の開発フローに沿って作業できます。このレッスンから始まる一連のレッスンでは、Issue を起点に機能を作成し、コードの妥当性と機能の動作を確認して、最終的にプロジェクトへマージする、一般的なエージェント主導の開発プロセスを体験します。

> [!NOTE]
> 機能開発のワークフローでは、同じ会話とブランチを続けて使います。通常、ファイルの種類ごとに異なるブランチや PR を使いますが、ここでは主要な概念に集中するため手順を簡略化しています。

このレッスンでは、次の作業を行います。

- GitHub Issue から Copilot の会話を開始します。
- Plan モードで要件を決めます。
- Autopilot モードで機能を実装します。
- コードをレビューします。
- 転送ブラウザーで機能を手動で検証します。

この機能の作業を続けながら、リポジトリの指示を更新し、既存の `quality-checks` スキルをカスタマイズし、MCP による検証を追加して QA エージェントを作成し、機能 PR を開きます。

## シナリオ

Tailspin Toys のカタログが増え、訪問者がゲームをカテゴリやパブリッシャーで絞り込めるようにする必要があります。バックログの Issue には機能が説明されていますが、カテゴリを組み合わせる方法など、コーディング前に合意が必要な詳細があります。Plan モードで方針を決めてから、範囲を定めた実装を Autopilot に任せます。

## 背景

AI コーディングエージェントを開発フローに導入しても、基本は変わりません。むしろ、基本の重要性は増します。多くの開発者は、次のような流れで作業します。

1. 実装内容を記載した Issue から始めます。
2. 実装計画を作成します。
3. コードを作成してレビューします。
4. テストを実行し、コードを検証します。
5. 新しい機能を手動で検証します。
6. プルリクエスト (PR) を作成します。
7. コードレビューと継続的インテグレーションが成功したら、コードをマージします。

> [!NOTE]
> 詳細な手順はチームや Organization によって異なりますが、ほとんどは上記の流れに沿っています。

この標準的な進め方に従うと、AI が生成したコードが要件を満たし、手作業で書いたコードと同じレビューと検証を受けるようになります。

## 会話モード

**会話モード**は、エージェントにどの程度の自律性を与えるかを制御します。<kbd>Shift</kbd>+<kbd>Tab</kbd> を押してモードを切り替えます。

- **Interactive**: エージェントが変更を提案し、次に進む前に利用者の入力を待ちます。
- **Plan**: エージェントが計画を作成します。計画モードではプロジェクトファイルを編集できません。
- **Autopilot**: エージェントがコードを書き、テストを実行し、タスクが完了するまで反復して自律的に作業します。

まず Plan モードで計画をレビューしてから、Autopilot で実装します。

## Issue から始める

絞り込みの作業を始める前に、Codespace に戻り、リポジトリとターミナルを準備します。

1. Codespace に戻ります。停止している場合は、再起動してから続けます。
2. 星評価の PR がマージされていることを確認します。
3. ターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
4. `main` を更新し、絞り込みの作業用ブランチを作成します。

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Copilot CLI を起動します。

   ```bash
   copilot --yolo
   ```

6. <kbd>Tab</kbd> を 2 回押して **Issues** タブを開きます。
7. <kbd>A</kbd> を押してすべての Issue を表示します。
8. 矢印キーを使い、**Allow users to filter games by category and publisher** というタイトルの Issue を選択します。
9. <kbd>C</kbd> を押して Issue をプロンプトに追加し、**Session** タブに戻ります。

プロンプトの先頭に `#7` (または同様の番号) が追加されます。`#` を使うと GitHub の Issue やプルリクエスト (PR) をコンテキストに追加できます。

## 絞り込み機能を計画する

計画を立てると、Copilot に機能の実装やタスクの実行を任せる前に方針を決められます。複雑な作業では、事前に少し時間をかけて計画を立てることをお勧めします。Plan モードに切り替え、Copilot に計画を作成させましょう。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Plan モードに切り替えます。プロンプトの下にあるモード表示が **Plan** になっていることを確認します。
2. 前の手順で追加した Issue の後に、次のプロンプトを入力します。

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot はプロジェクトを調べ、最適な方法を検討して計画を作成します。

3. 作業中に、絞り込み機能の動作について質問されることがあります。希望に基づいて回答してください。答えに正解・不正解はありません。
4. 計画が完成したら、<kbd>Control</kbd>+<kbd>E</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) を押して計画を展開します。
5. 計画を読み、内容を確認します。
6. 希望と異なる部分があれば、Copilot に計画の修正を依頼します。

## Autopilot を承認する

計画の作成とレビューが終わったら、実装に進みます。Autopilot を使って Copilot に作業を任せます。Autopilot では、Copilot が完了したと判断するまで問題に取り組みます。

1. **Accept plan and build on autopilot (recommended)**、またはインストール済みのバージョンに表示される同様のオプションを選択します。
2. プロンプトの下にあるモード表示が **Autopilot** になっていることを確認します。
3. Copilot が計画に沿って反復し、コードを生成してテストを実行する様子を確認します。

> [!NOTE]
> 承認するとすぐに実装が始まることがあります。先に計画をレビューしてください。依存関係が不足している、またはポートが競合していると Copilot が報告した場合は、チェック完了とみなす前にセットアップの問題を解決してください。

## 実装をレビューして検証する

コードの生成後は、他のコードと同様にマージ前にレビューします。コードをレビューしてサイトを実行し、問題がないことを確認します。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Interactive モードにします。モード表示が **Plan** または **Autopilot** ではないことを確認します。
2. `/diff` を入力し、絞り込みの実装とテストを確認します。
3. Issue と、計画時に決定した内容に照らし合わせます。
4. コードレビュー後、<kbd>Esc</kbd> を押して差分画面を閉じます。
5. プロジェクトのチェック結果を確認し、失敗があれば Copilot に修正を依頼します。

## 新機能を確認する

コードがよさそうでも、実際に動くか確認しましょう。前と同じようにアプリを起動し、Codespaces の転送ポートからサイトを開きます。

1. Copilot にアプリの起動を依頼します。

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces でポート `4321` が利用可能になったら **Open in Browser** を選択します。
3. 計画で決めたカテゴリとパブリッシャーの絞り込み、およびその組み合わせを試します。
4. リセット時と検索結果がない場合の動作が、Issue と決定内容に合っていることを確認します。
5. Codespace に戻り、起動した開発サーバーを停止するよう Copilot に依頼します。

## まとめと次のステップ

会話モードを切り替えて機能を作成し、レビューしました。このレッスンでは、次の作業を行いました。

- GitHub Issue から Copilot の会話を開始しました。
- Plan モードで要件を決めました。
- Autopilot モードで機能を実装しました。
- コードをレビューしました。
- 転送ブラウザーで機能を手動で検証しました。

次は、文書化されたプラクティスに沿ってコードを生成するため、[カスタム指示を使用します][next-lesson]。

## リソース

- [GitHub Copilot CLI の Autopilot][autopilot]
- [Copilot CLI コマンド リファレンス][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
