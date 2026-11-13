---
title: "演習 5: GitHub Copilot の作業を反復して改善する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

## 作業をレビューする

このラボでは、ユーザー体験の改善や機能の追加を目的とした複数のタスクを GitHub Copilot と一緒に行いました。コードへのドキュメント追加、デザインチーム向けの関連ゲーム機能の作成、ハイコントラストとライトモードの切り替えを含むアクセシビリティ機能の実装を依頼しました。コードの変更を確認し、必要に応じて Copilot にフィードバックを送り、改善しましょう。

### シナリオ

ここまでに何度も確認したとおり、生成 AI を導入しても、ソフトウェア設計と DevOps の基本は変わりません。生成されたコードをレビューし、通常の DevOps プロセスを行う必要があります。チームメンバーがレビューできるようにする前に、ドキュメント、関連ゲーム機能、アクセシビリティ機能に関して GitHub Copilot が提案した内容を確認します。

## GitHub Copilot cloud agent のセキュリティ

Copilot cloud agent は非同期に、監督を受けずに作業するため、安全性を保つための制約があります。

- Copilot はリポジトリへの読み取りアクセス権を持ち、書き込みできるのは作業に使用するブランチだけです。
- Cloud agent は GitHub Actions 内で動作し、作業用の一時的な環境を作成します。
- GitHub Actions ワークフローの実行には、人間による承認が必要です。
- MCP サーバーなど、[既定では外部リソースへのアクセスが制限されます](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)。

## 生成されたドキュメントをレビューする

最初に、GitHub Copilot cloud agent が作成した、コードへのドキュメント追加のプルリクエスト (PR) を確認します。GitHub.com の標準的な PR インターフェイスを使います。

> [!NOTE]
> PR に GitHub Copilot がファイアウォールでブロックされたという警告が表示されることがあります。Copilot は MCP サーバーなどの外部リソースへのアクセスが既定で制限されているため、これは**想定どおり**です。必要であれば、[Copilot cloud agent のファイアウォールをカスタマイズまたは無効化][agent-firewall]できます。

1. github.com のリポジトリに戻ります。
2. **Pull Requests** を選択して PR の一覧を開きます。
3. **Add missing documentation** などのタイトルの PR を開きます。

> [!NOTE]
> Copilot がまだ作業中の場合、PR のタイトルに **[WIP]** が含まれます。その場合は作業が完了するまで待ちます。数分かかることがあります。その間に休憩したり、これまでに学んだ内容を振り返ったりしてください。

4. 準備ができたら **Files changed** タブを選択し、変更をレビューします。

    ![Files changed タブ](../../../_images/shared-pr-files-changed.png)

5. 新しく追加された TSDoc のドキュメントコメントや、その他のドキュメントを確認します。具体的な変更内容は異なる場合があります。レビューでは、Exercise 2 の最初に確認したカスタム指示ファイルから追加された TSDoc コメント、TypeScript の規約、コメントヘッダーに注目します。
6. 問題がなければ **Conversation** タブに戻り、下へスクロールします。
7. ワークフローの承認待ちを示す表示を確認します。
8. ワークフローの承認待ちがある場合は、**Approve and run workflows** を選択します。

   ![ワークフローを承認して実行する画面](../../../_images/shared-approve-workflows.png)

9. PR のチェック欄にワークフローが追加されます。問題がなければ、単一 Astro アプリのプロジェクトチェックが成功します。完了まで数分かかることがあります。

## GitHub Copilot に変更を依頼する

Copilot との PR 作業は一方通行ではありません。チームメンバーに依頼するのと同じように、PR やコードへのインラインコメントで Copilot にメンションできます。Copilot はコメントを確認し、要求に対応する新しいセッションを開始します。結果は確率的に変わるため、依頼する文章を厳密に指定することはできません。たとえば、次のような変更を依頼できます。

- 各コードファイルの先頭に、内容を簡単に説明するコメントヘッダーを追加する。
- TypeScript と Astro ファイルに TSDoc のドキュメントコメントを追加する。
- Astro アプリの構造を説明する README を作成する。

1. 上記の案や、コードベースに追加してほしいドキュメントについての提案を使い、**@copilot** にメンションして生成されたドキュメントの変更を依頼するコメントを追加します。
2. **View Session** を選択して Copilot の作業を確認します。Copilot が更新用の新しいセッションを開始します。
3. **Back to pull request** を選択すると PR に戻れます。

    ![プルリクエストに戻る](../../../_images/ex7-back-to-pr.png)

4. Copilot の変更が完了すると、PR に新しいコミットが表示されます。
5. **Files changed** タブを選択して変更をレビューします。

満足するまで反復して改善できます。準備ができたら、ドラフト PR をレビュー可能な状態にして、`main` ブランチにマージします。

![PR をレビュー可能な状態にする画面](../../../_images/ex7-ready-for-review.png)

## 関連ゲーム機能をレビューする

ゲーム詳細ページに関連ゲームを表示する Issue を解決するため、Copilot が作成した PR を確認します。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Show related games on the game details page** などのタイトルの PR を選択します。
4. **Files changed** タブを選択して、生成されたコードをレビューします。
5. 問題がなければ **Conversation** タブに戻り、下へスクロールします。
6. ワークフローの承認待ちを示す表示を確認します。
7. 承認待ちのワークフローがある場合は **Approve and run workflows** を選択します。

   ![ワークフローを承認して実行する画面](../../../_images/shared-approve-workflows.png)

8. PR のチェック欄にワークフローが追加されます。問題がなければ、単一 Astro アプリのプロジェクトチェックが成功します。完了まで数分かかることがあります。
9. **任意:** Codespace でこのブランチに切り替え、関連ゲーム機能を手動でテストできます。Codespace でターミナルを開き、Copilot が作成したブランチ名 (例: **copilot/fix-8**) に `<branch-name>` を置き換えて、次のコマンドを実行します。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot が関連ゲーム機能を作成しました。前と同じように、Copilot cloud agent に追加の変更を依頼できます。たとえば、表示する関連ゲームの数を調整したり、コメントヘッダーと TSDoc のドキュメントコメントを追加したりできます。この作業はカスタム指示を更新する**前**に割り当てたことを思い出してください。これまでと同様に **Conversation** タブでコメントを追加すると、Copilot が内容を確認して新しいセッションを開始します。

## アクセシビリティ機能をレビューする

最後に、アクセシビリティカスタムエージェントで実装した機能をレビューします。この PR には、Exercise 3 で依頼したハイコントラストモードと、Exercise 4 で Mission control から追加を依頼したライトモードの両方が含まれているはずです。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Add high contrast mode to website** などのタイトルの PR を選択します。

> [!NOTE]
> Copilot がまだ作業中の場合、PR のタイトルに **[WIP]** が含まれます。その場合は作業が完了するまで待ちます。数分かかることがあります。

4. **Files changed** タブを選択して、生成されたコードをレビューします。
5. 実装をレビューします。特に次の点を確認します。
   - モードを切り替える UI コンポーネント。
   - ユーザー設定の保存に使うローカルストレージ。
   - ハイコントラストモードとライトモードの CSS またはスタイルの変更。
   - アクセシビリティ属性 (ARIA ラベル、キーボード操作など)。
   - モードの切り替えを処理する JavaScript/TypeScript コード。
6. 問題がなければ **Conversation** タブに戻り、下へスクロールします。
7. ワークフローの承認待ちを示す表示を確認します。
8. 承認待ちのワークフローがある場合は **Approve and run workflows** を選択します。

   ![ワークフローを承認して実行する画面](../../../_images/shared-approve-workflows.png)

9. PR のチェック欄にワークフローが追加されます。問題がなければ、単一 Astro アプリのプロジェクトチェックが成功します。完了まで数分かかることがあります。
10. **任意:** Codespace でブランチをチェックアウトし、アクセシビリティ機能を手動でテストできます。Codespace でターミナルを開き、Copilot が作成したブランチ名に `<branch-name>` を置き換えて、次のコマンドを実行します。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    アプリを起動し、ブラウザーでハイコントラストとライトモードの切り替えをテストします。ページを再読み込みしても設定が保存されることを確認します。

アクセシビリティカスタムエージェントによって、Copilot はアクセシビリティのベストプラクティスに沿って機能を実装できました。アクセシビリティに関する懸念や改善点があれば、これまでと同じようにコメントで **@copilot** に変更を依頼できます。

## 任意の演習 — さらに作業を委任する

実際のバックログ項目をエージェントに任せ、自分は別の作業に取り組めると cloud agent を効果的に活用できます。習慣を身につけるために、リポジトリに Issue を追加して Copilot に割り当ててみましょう。次のような案があります。

- ゲーム詳細ページに支援者向けの関心フォームを作成する。
- ゲーム一覧ページにページネーションを実装する。
- データアクセスヘルパーに入力検証とエラー処理を追加する。

## まとめ

Cloud agent ハーネスを完了しました。これらのレッスンでは、次の作業を行いました。

- **リポジトリに付属するカスタム指示ファイルを確認し**、後で cloud agent の出力に与える影響を確認しました。
- **GitHub Issue を Copilot cloud agent に割り当て**、環境の準備、計画、非同期の実行を確認しました。
- **アクセシビリティ用のカスタムエージェントを作成して使い**、ハイコントラストとライトモードの切り替えを追加しました。
- **Copilot agents ページを Mission control として使い**、作業中のアクセシビリティセッションを監視して方向付けました。
- **cloud agent のプルリクエストをレビューして改善し**、`@copilot` に変更を依頼し、ワークフローを承認しました。

## レビューと次のステップ

Cloud agent ハーネスを完了しました。さらに学ぶ場合は、次のハーネスも役立ちます。

- 🖥️ **[VS Code ハーネス](../../vscode/)** — IDE から Copilot Chat のエージェントモードと MCP の統合を学びます。
- 💻 **[CLI ハーネス](../../cli/)** — Plan と Autopilot モード、エージェントスキル、QA カスタムエージェント、Playwright MCP、Agent Merge、任意の `/delegate` による cloud agent との連携を使い、ターミナルからレビュー済みの変更を 2 件リリースします。

自分のリポジトリでは、次のような作業も試せます。

- リファクタリングやテスト範囲の拡大を Issue にして cloud agent に割り当てる。
- 別の分野向けのカスタムエージェントを作成する。
- 異なるスタック向けに `copilot-setup-steps.yml` を設定する。

## リソース

- [GitHub Copilot][github-copilot]
- [Copilot エージェントについて][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップワークフローに関するベストプラクティス][cloud-agent-best-practices]
- [Copilot cloud agent のファイアウォールを設定する][agent-firewall]

---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
