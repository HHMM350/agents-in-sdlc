---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

技術的負債に悩まされていない組織は、ほとんどありません。未解決のセキュリティ課題、更新が必要なレガシーコード、実装する時間がなくバックログに残った機能リクエストなどがあります。GitHub Copilot の cloud agent は、コードの更新や機能の追加などを自律的に行います。エージェントは作業の完了後、開発者がレビューできるドラフト PR を作成します。こうした手間のかかる作業を任せることで、開発を加速し、より大きな課題に集中できます。

Copilot cloud agent を使って、次の内容を学びます。

- コード生成用の環境をカスタマイズする方法。
- 操作を安全に行う方法。
- Issue の範囲を明確に定義する重要性。
- Issue を Copilot に割り当てる方法。

## シナリオ

Tailspin Toys には解決したい技術的負債があります。最初のサイトを作成した委託先がドキュメントを十分に作成しておらず、実質的にドキュメントがありません。まず、アプリケーションのエクスポートされたすべての関数に TSDoc のドキュメントコメントを追加します。

また、デザインチームはゲームを見つけやすくしたいと考えています。各ゲームの詳細ページに、同じカテゴリに属する関連ゲームを表示して、利用者がほかのゲームも引き続き閲覧できるようにします。まだ完成度の高い実装は必要なく、UX の受け入れテストに使える状態にしたいと考えています。これは現在のブロッカーですが、優先度の高い Issue がほかにもあります。

優先度が下がりやすいこのような作業は、Copilot cloud agent に割り当てるのに適しています。エージェントが非同期で作業している間に別の作業を進め、後から戻って結果をレビューできます。

## GitHub Copilot cloud agent について

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) は、人間の開発者のようにバックグラウンドで作業できます。たとえば[GitHub Issue を Copilot に割り当てる][assign-issue]方法があります。割り当てると、Copilot は進捗を記録するドラフト PR を作成し、環境を準備して作業を開始します。作業中も完了後もセッションを確認できます。提案された解決策のレビュー準備ができると、プルリクエストで通知されます。

## 範囲を明確にした指示の重要性

GitHub Copilot に魔法はありません。考える作業を省略できるわけではありません。一見簡単そうな作業にも、掘り下げると複雑さが潜んでいます。[Copilot cloud agent に依頼するタスクの範囲][cloud-agent-best-practices]を慎重に決めてください。AI ペアプログラマーとして扱い、段階を踏んで学び、試し、調整します。生成 AI を導入しても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム指示

前の演習では、カスタム指示とその活用方法を学びました。`.github/copilot-instructions.md` を使ったことがあれば効果を確認できています。まだの場合は、cloud agent に作業を割り当てる前に、このリポジトリに用意された指示ファイルを読み取り専用で確認して、後から影響を確認できるようにします。

GitHub Web UI または起動済みの Codespace で、次のファイルを開きます。

- `.github/copilot-instructions.md` - **Code standards** セクションで、TypeScript の規約と TSDoc コメントの要件を確認します。
- `.github/instructions/unit-tests.instructions.md` - `applyTo` frontmatter を確認します。この指示は `**/*.test.ts` ファイルに適用されます。

次のセクションで `Code lacks documentation` Issue を cloud agent に割り当てたら、生成された PR に TSDoc コメント、TypeScript の規約、コメントヘッダーがあるかを確認します。後の演習で PR をレビューする際にも取り上げます。

## Copilot cloud agent の開発環境を設定する

コードの作成には、誰が作業する場合でも、適切な環境と初期セットアップが必要です。Copilot にタスクを割り当てる場合も同様です。cloud agent はソフトウェアエンジニアのように作業します。

Cloud agent は [GitHub Actions][github-actions] の環境を使います。`.github/workflows/copilot-setup-steps.yml` に設定した[専用のセットアップワークフロー][setup-workflow]で、必要な開発ツールや依存関係を事前に準備できます。ワークショップの流れを簡単にし、学習の機会を設けるため、事前に構成済みです。Node.js、プロジェクトの依存関係、E2E テスト用のブラウザーバイナリ、単一 Astro アプリ用にマイグレーションと初期データ投入を済ませた SQLite データベースを利用できます。

```yaml
name: "Copilot Setup Steps"

# リポジトリの "Actions" タブからセットアップ手順をテストできます
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # *各手順*に必要な最小限の権限を設定します。Copilot の操作には専用のトークンが使われます。
    permissions:
      # 依存関係のインストールなど、セットアップ手順でリポジトリをクローンする場合は `contents: read` 権限が必要です。セットアップ手順でクローンしない場合は、手順の完了後に Copilot が自動的にクローンします。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / アプリのセットアップ - Node.js (アプリ全体は Astro + Drizzle/libSQL で構成されています)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # ビルドとテストでデータを利用できるよう、ローカルの SQLite データベースをマイグレーションして初期データを投入します。
      - name: Set up the database
        run: npm run db:setup
```

一般的な GitHub ワークフローファイルと同じ形式ですが、次の点に注意してください。

- `copilot-setup-steps` という単一のジョブがあります。Copilot が PR の作業を始める前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーを使うと、リポジトリの **Actions** タブからワークフローを手動実行できます。Copilot の実行を待たずに、正常に動くかテストできます。

## ドキュメントを追加する

ドキュメントが重要なのは誰もが理解していますが、情報が古かったり不足していたりするプロジェクトは少なくありません。こうした技術的負債は放置されやすく、生産性を下げ、コードベースの保守や新メンバーの受け入れを難しくします。Copilot はドキュメントの作成が得意なため、cloud agent に割り当てるのに適した Issue です。エージェントがバックグラウンドで必要なドキュメントを作成します。後の演習で結果をレビューします。

1. 新しいブラウザータブで github.com のリポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択して新しい Issue のダイアログを開きます。
4. **Blank issue** を選択して Issue を作成します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次の内容を入力します。

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. **Create** を選択して Issue を作成します。
8. 右側の **Assign to Copilot** を選択して割り当てダイアログを開きます。

   ![Issue に Copilot を割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

   ![Copilot の割り当て詳細](../../../_images/ex4-assign-copilot-details.png)

10. **Pull Requests** タブを選択します。
11. 新しく作成されたプルリクエスト (PR) を開きます。タイトルは `[WIP]: Code lacks documentation` のようになります。PR が一覧に表示されない場合は、少し待ってからブラウザーを更新してください。
12. 数分後、Copilot が TODO リストを作成します。

> [!NOTE]
> Copilot の TODO リストが PR に表示されるまで数分かかる場合があります。前述のワークフローを使って環境を作成し、プロジェクトを分析して、最適な方法を検討しています。

13. リストを確認し、実行するタスクを確認します。
14. プルリクエストのタイムラインを下へスクロールし、Copilot が Issue の作業を開始したことを確認します。
15. **View session** ボタンを選択します。

   ![Copilot セッションの表示](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 表示が更新されない場合は、ブラウザーを更新してください。

16. ライブセッションをスクロールして Copilot の作業を確認します。コードを調査して状態を把握し、計画を検討してからコードを作成する様子を確認できます。

作業には数分かかることがあります。Copilot cloud agent の主な利点は、非同期にタスクを実行し、その間に別の作業を進められることです。別の作業を割り当てて、アプリに機能を追加するコードを書きながらこの利点を活用します。

## ゲーム詳細ページに関連ゲームを追加する

GitHub Copilot cloud agent の大きな利点の 1 つは、作業を分けられることです。デザインチームが求める関連ゲームの表示は長時間かからないかもしれませんが、その時間を別の作業に使えます。Copilot cloud agent に割り当てましょう。

1. github.com のリポジトリに戻ります。
2. **Issues** タブを選択します。
3. **New issue** を選択して新しい Issue のダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次の内容を入力します。

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. **Create** を選択して Issue を作成します。
8. 右側の **Assign to Copilot** を選択して割り当てダイアログを開きます。

   ![Issue に Copilot を割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

最初のコメントに 👀 が表示され、Copilot が作業中であることを示します。

![目の絵文字で Copilot が Issue に取り組んでいることを示す画面](../../../_images/ex4-issue-eyes-emoji.png)

Copilot は 2 件目のリクエストにも取り組んでいます。cloud agent はソフトウェアエンジニアと同じように作業するため、常に監視する必要はありません。作業後にレビューします。次はカスタムエージェントを作成して使います。

## まとめと次のステップ

このレッスンでは [GitHub Copilot cloud agent][copilot-agents]を学びました。cloud agent に Issue を割り当て、非同期に作業させることができます。技術的負債への対応、新機能の作成、別のフレームワークへのコード移行などに活用できます。

次の内容を学びました。

- コード生成用の環境をカスタマイズする方法。
- 操作を安全に行う方法。
- Issue の範囲を明確に定義する重要性。
- Issue を Copilot に割り当てる方法。

cloud agent がバックグラウンドで作業している間に、カスタムエージェントを作成して使用します。[Copilot cloud agent は MCP サーバーも利用でき][cloud-agent-mcp]、前のモジュールで学んだカスタム指示にも対応しています。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップワークフローに関するベストプラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタムエージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
