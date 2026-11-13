---
title: "演習 2 - Copilot エージェントモードで機能を追加する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

アプリケーションの小さな更新でも、複数のファイル変更やテスト実行が必要になる場合があります。必要なファイルを探して変更し、テストを実行し、問題をデバッグし、変更漏れに気づいて再度更新する、という作業が続きます。

Copilot Agent Mode を使うと、IDE の中でより自律的に作業できます。開発者と同じように、既存のプロジェクト構成を調べ、必要なファイルを更新し、テストなどのタスクを実行し、発見した問題を自動的に修正します。Agent Mode を使ってサイトに機能を追加する方法を確認しましょう。

Copilot Agent Mode は IDE 内で動作するため、すばやくやり取りしながら作業できます。エージェントモードと cloud agent は名前が似ていますが、異なる体験を提供します。エージェントモードは IDE 内で作業し、cloud agent は Issue やプルリクエストを通じてチームの一員のように非同期で作業します。

この演習では、次の内容を学びます。

- Copilot Agent Mode がプロジェクトを調査し、関連ファイルを特定して、複数のファイルを連携して変更する方法。
- GitHub Copilot Agent Mode で UI とデータ層にまたがる機能を実装する方法。
- コードベースにマージする前に、Copilot Agent Mode が生成した変更とテストをレビューする方法。

## シナリオ

ゲームの一覧が増えてきたため、カテゴリとパブリッシャーで絞り込めるようにします。前の演習ですでに publisher ヘルパーを追加しました。残りのデータ層、UI、テストを Copilot Agent Mode で完成させます。

## Tailspin Toys の Web サイトを実行する

変更を加える前に、Tailspin Toys の Web サイトを確認し、現在の機能を理解しましょう。

この Web サイトは、開発者をテーマにしたボードゲームのクラウドファンディングプラットフォームです。ゲームの一覧や詳細を表示します。Astro アプリケーションはビルド時にページを静的 HTML として生成します。ページは frontmatter 内で Drizzle ORM を通じてローカル SQLite データベースを直接参照します。個別のバックエンド API やクライアント側 UI フレームワークはありません。再利用可能なデータアクセスヘルパーは `src/lib/` にあり、Astro の `<script>` 内で標準 DOM API を使って限定的なインタラクティブ機能を追加します。

### Web サイトを起動する

`npm run dev` タスクを使うと、単一の Astro 開発サーバーを起動できます。GitHub Codespace で次の手順を実行します。

1. Codespace に戻ります。前の演習を終えて `main` に戻っているはずです。
2. Codespace 内で <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して新しいターミナルを開きます。
3. 絞り込み機能の新しいブランチを作成して切り替えます。

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 次のコマンドを実行して Web サイトを起動します。

   ```bash
   npm run dev
   ```

   Astro 開発サーバーが起動すると、次のような URL が表示されます。

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> `http://localhost:4321` を開くよう促すダイアログが表示された場合は、**x** を選択して閉じます。

5. ターミナルに表示された Astro サーバーのアドレス `http://localhost:4321` を、<kbd>Command</kbd> (Mac) または <kbd>Ctrl</kbd> (Windows/Linux) を押しながら選択して Web サイトを開きます。

> [!NOTE]
> Codespace のターミナルで localhost の URL を選択すると、自動的に `https://<your-codespace-name>-4321.app.github.dev/` に転送されます。これは Codespace でホストされる Web サーバーへのプライベートなトンネルです。

### Web サイトを確認する

Web サイトを起動したら、次の機能を確認します。

- **ホームページ**: タイトル、画像、説明を含むボードゲームの一覧を表示します。
- **ゲーム詳細ページ**: ゲームを選択すると、タイトル、説明、パブリッシャー、カテゴリなどの詳細が表示されます。

## Copilot でバックログを調べる

> [!TIP]
> **Copilot Chat を開く**
>
> 以下の演習を始める前に Codespace に戻り、Copilot Chat パネルを開いて **New Chat** を選択し、新しい会話を始めてください。モードとモデルの選択は演習によって異なります。必要な場合は各手順で説明します。

Web サイトは動作しますが、新しい機能で強化したいと考えています。まずバックログを確認しましょう。テンプレートからプロジェクトを作成すると、Issue のバックログも自動的に用意されます。GitHub Copilot に内容を表示させます。

1. Chat ビューのエージェント一覧で **Agent** を選択します。エージェントモードでは、ファイルをまたいだ計画と実装、ターミナルコマンド、ツールの利用を自律的に行います。

   ![Chat ビューのエージェント選択メニューのスクリーンショット。](../../../_images/shared-chat-mode-selector.png)

2. 利用可能なモデル一覧から **Claude Sonnet 4.5** を選択します。

> [!CAUTION]
> このワークショップは、特定のモデルを推奨するものではありません。作成時に Claude Sonnet 4.5 を使用しており、安定した体験になるよう手順に記載しています。ただし LLM の動作は確率的であるため、提案は例と異なる場合があります。これは通常の動作です。

> [!NOTE]
> 確率的な動作のため、Copilot が別の MCP コマンドを使う場合がありますが、タスクは実行できます。

3. 次のプロンプトを送信し、GitHub Copilot に Issue のバックログを尋ねます。

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. **Continue** を選択して、Issue の一覧表示コマンドを実行します。
5. 生成された Issue の一覧を確認します。

Copilot が利用者にとって有益だと考える順に優先度を付けたことを確認します。

## 指示ファイルをレビューする

コードの生成をエージェントに依頼する前に、作業のコンテキストを与える指示ファイルを確認します。Web サイトの機能追加に関するガイダンスを含む [UI 指示ファイル](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)を使います。

1. Codespace で `.github/instructions/ui.instructions.md` を開きます。
2. 機能追加に関する全体的なガイダンスを確認します。アーキテクチャの概要、コンポーネントの設計・テスト可能性・アクセシビリティの原則、ファイル種類に応じた Astro、Tailwind CSS、Drizzle の指示へのリンクがあります。

> [!TIP]
> 指示ファイルから、他の指示ファイルやプロジェクト内のファイルを参照できます。パスは指示ファイルからの相対パスです。再利用、複雑な指示の分割、例やテンプレートの提示に役立ちます。

## 絞り込み機能を実装する

絞り込みを完成するには、少なくとも次の 3 つを更新します。

- データ層 (`src/lib/`) の絞り込みロジックを追加または改善します。
- 絞り込み動作のテストを追加または更新します。
- ゲーム一覧ページに絞り込み UI を追加します。

コードベースにマージする前にテストを実行し、成功させる必要があります。Copilot Agent Mode にこれらの作業を依頼しましょう。

1. Copilot との現在の会話を続けるか、**New Chat** を選択して新しい会話を始めます。
2. **Add Context**、**Instructions**、**ui** の順に選択して UI 指示ファイルを追加します。

   ![UI 指示ファイルを選択する例を示すスクリーンショット](../../../_images/ex3-select-instructions-file.png)

3. Chat ビューのエージェント一覧で **Agent** が選択されていることを確認します。

   ![Chat ビューのエージェント選択メニューのスクリーンショット。](../../../_images/shared-chat-mode-selector.png)

4. モデルが **Claude Sonnet 4.5** のままであることを確認します。
5. バックログの関連 Issue に基づいて機能を実装するよう、次のプロンプトで Copilot に依頼します。

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Copilot がプロジェクトを調べ、機能に関係するデータ層ヘルパー、UI、テストを見つけ、ファイルを更新してテストを実行する様子を確認します。

   ![Copilot がプロジェクトファイルを調査しているスクリーンショット](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot はプロジェクトの調査、ファイルの編集、テストの実行などを行うため、作業には数分かかることがあります。作業中、コードエディターに **Keep** と **Undo** が表示される場合があります。完了後はすべての変更に **Keep** または **Undo** が表示されます。処理の途中で選択する必要はありません。

7. Copilot に求められたら **Continue** を選択してテストを実行します。

   ![Copilot Chat でテスト実行の確認を求めるダイアログ](../../../_images/ex3-agent-mode-run-tests.png)

8. 作業中に停止したり、テストが失敗したりすることがあります。問題ありません。Copilot はタスクを完了し、エラーがないと判断するまでコード生成とテストを繰り返します。

   ![Copilot Agent Mode の完了したチャットセッション](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 生成されたコードに問題がないか確認します。

> [!CAUTION]
> Copilot などの AI ツールが生成したコードは、必ずレビューしてください。

10. Web サイトを開いているブラウザーに戻り、新機能を試します。
11. 動作とコードを確認したら、Copilot Chat ウィンドウで **Keep** を選択します。

## まとめと次のステップ

この演習では、GitHub Copilot Agent Mode を使って Tailspin Toys の Web サイトに機能を追加する方法を学びました。

- GitHub Copilot Agent Mode で UI とデータ層にまたがる新機能を実装できます。
- Copilot Agent Mode はプロジェクトを調査し、関連ファイルを特定して、複数ファイルを連携して変更できます。
- コードベースにマージする前に、Agent Mode が生成した変更とテストをレビューします。

次は[Playwright MCP サーバーで機能をテストし][next-lesson]、プルリクエストを作成します。

### 追加の演習 — ページネーションを実装する

ゲーム一覧が増えるとページネーションが必要になります。この演習で学んだ方法を使って、Copilot にページネーションを実装させましょう。次の点を検討してください。

- 既存の指示ファイルを使うなど、ベストプラクティスに従います。
- ユーザーがページサイズを選べるようにするか、固定値にするかを決めます。
- 希望する実装に必要なガイダンスを、プロンプトで Copilot に伝えます。
- 変更を依頼してコンテキストを補足しながら、Copilot と反復して作業することがあります。これは通常の進め方です。

## リソース

- [Copilot の Ask、Edit、Agent モード: 機能と使い分け][choose-mode]
- [VS Code のエージェントモード][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
