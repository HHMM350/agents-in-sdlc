---
title: "演習 3 - Playwright MCP サーバーで機能をテストする"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: エージェントモード][previous-lesson] · [次のレッスン: カスタムエージェント →][next-lesson]

エージェントモードで絞り込み機能を作成しました。プルリクエストを開く前に、ブラウザーで実際に動くことを確認しましょう。自分でアプリを操作する代わりに、**Playwright MCP サーバー**を接続し、Copilot に実際のブラウザーを操作させて機能をテストします。その後、ブランチを公開して PR を作成します。

この演習では、次の作業を行います。

- Model Context Protocol (MCP) と、MCP サーバーで Copilot にツールを追加する方法を学びます。
- Playwright MCP サーバーをワークスペースに追加します。
- ブラウザーで絞り込み機能を手動テストするよう Copilot に依頼します。
- ブランチを公開し、絞り込み機能のプルリクエストを作成します。

## Model Context Protocol (MCP) とは

エージェントモードは、エディターの外にアクセスできるとさらに便利です。Model Context Protocol (MCP) は、Copilot が外部のツールやサービスと通信するための標準的な方法です。

![エージェントモードとコンテキスト、LLM、MCP サーバーや VS Code 拡張機能が提供するツールの連携を示す図](../../../_images/ex1-mcp-diagram.png)

[Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) は、AI エージェントが外部のツールやサービスと通信するための仕組みです。MCP を使うと、AI エージェントはリアルタイムで最新情報にアクセスしたり、ツールを使ってユーザーに代わって操作を実行したりできます。

MCP サーバーは、AI エージェントと外部のツールやサービスの間を仲介します。既存の API や npm パッケージなどのローカルツールとエージェントの通信を管理します。各 MCP サーバーが、エージェントから利用可能なツールやリソースを提供します。

よく使われる MCP サーバーには、次のものがあります。

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)**: GitHub リポジトリを管理する API を利用できます。新しいリポジトリの作成、既存リポジトリの更新、Issue やプルリクエストの管理などを AI エージェントに依頼できます。
- **[Playwright MCP Server](https://github.com/microsoft/playwright-mcp)**: Playwright によるブラウザー自動化機能を利用できます。Web ページを開き、フォームに入力して、ボタンを選択するなどの操作ができます。

ほかにも多くの MCP サーバーがあります。エコシステム内での発見や貢献を促進するために、GitHub は [MCP レジストリ](https://github.com/mcp)をホストしています。

> [!CAUTION]
> セキュリティ上、MCP サーバーは他の依存関係と同じように扱ってください。利用前にソースコードを確認し、発行者を検証して、セキュリティへの影響を検討します。信頼できる MCP サーバーだけを利用し、機密リソースや操作へのアクセスを許可する際は注意してください。

## MCP の構成を確認する

`.vscode/mcp.json` ファイルで、この VS Code ワークスペースから利用できる MCP サーバーを設定します。

1. Codespace で `.vscode/mcp.json` を開きます。
2. すでに `github` サーバーが設定されています。

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        }
      }
    }
    ```

`github` の設定はプロジェクトテンプレートに含まれています。そのため、前の演習で Copilot は Issue のバックログを読み取れました。[リモート GitHub MCP サーバー][remote-github-mcp-server]を使うため、ローカルへのインストールは不要です。VS Code は HTTP で接続し、Copilot が最初にツールを使うときに GitHub で認証します。

## Playwright MCP サーバーを追加する

次に 2 つ目のサーバーを追加します。[Playwright MCP サーバー][playwright-mcp-server]を使うと、Copilot が操作できるブラウザーを提供できます。機能のテストに最適です。

1. `.vscode/mcp.json` の `github` と並べて `playwright` の設定を追加し、ファイルが次のようになるようにします。

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        },
        "playwright": {
          "command": "npx",
          "args": ["@playwright/mcp@latest", "--headless"]
        }
      }
    }
    ```

2. ファイルを保存します。

リモートの `github` サーバーとは異なり、`playwright` はローカルサーバーです。VS Code が `npx @playwright/mcp@latest` を実行して起動します。`--headless` フラグを指定すると、画面を表示せずにブラウザーを実行します。Codespace には表示用デスクトップがないため必要です。

> [!NOTE]
> Tailspin Toys では E2E テストに Playwright を使用しているため、必要なブラウザーはすでにインストールされていることが多いです。Copilot がブラウザーの不足を報告した場合は、`npx playwright install chromium` を実行して再試行するよう依頼します。

## サーバーを起動して信頼する

VS Code は必要に応じて MCP サーバーを起動します。Copilot が初めてサーバーのツールを使うときにサーバーを起動し、信頼するか確認します。

1. `.vscode/mcp.json` の `playwright` 設定の上に **Start** が表示されます。選択するとサーバーが起動し、設定を確認できます。
2. VS Code からサーバーを信頼するか尋ねられたら、設定を確認して、起動を許可する場合は信頼を選択します。

手動で起動する必要はありません。省略した場合は、次の手順で Copilot がツールを最初に使うときに VS Code が起動し、信頼を確認します。

## 絞り込み機能をテストする

[Playwright MCP サーバー][playwright-mcp-server]は、Copilot が操作できる実際のブラウザーを提供します。利用者がアプリを操作しなくても、エージェントがページを開き、移動し、絞り込みを適用して結果を読み取り、確認した内容をまとめます。会話を離れずに機能を検証できます。

Playwright MCP サーバーはスクリーンショットではなく、ページの[アクセシビリティツリー][playwright-mcp-server]を使います。エージェントはボタン、リンク、リスト項目など、ラベル付きの構造化された要素を使って判断します。支援技術と同じ要素を調べるため、簡単な機能確認がアクセシビリティの基本確認にもなります。

サーバーを接続してアプリを起動した状態で、作成した絞り込み機能をテストするよう Copilot に依頼します。

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

Copilot は Playwright MCP サーバーを通じてブラウザーを起動し、各手順を実行して結果を報告します。レポートを Issue の受け入れ条件に照らし合わせます。問題がある場合は、プルリクエストを作成する前に追加の質問をしたり、コードの修正を依頼したりします。

> [!NOTE]
> テストするには、アプリが `http://localhost:4321` で実行されている必要があります。開発サーバーを停止している場合は、プロンプトを送信する前にもう一度起動します。Playwright MCP サーバーを初めて使う際、ブラウザーのダウンロードが必要になる場合があります。ブラウザーが見つからないと報告されたら、`npx playwright install chromium` を実行して再試行するよう依頼します。

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## ブランチを公開してプルリクエストを作成する

機能が動作することを確認したので、チームにレビューしてもらう PR を作成します。まず `filtering-vscode` ブランチを公開します。

1. Codespace の **Source Control** パネルに移動し、Copilot が行った変更をレビューします。
2. **+** アイコンを選択して変更をステージします。
3. **Sparkle** ボタンを使ってコミットメッセージを生成します。

   ![変更を表示する Source Control パネルのスクリーンショット](../../../_images/ex3-source-control-changes.png)

4. **Publish** を選択してブランチをリポジトリにプッシュします。

## プルリクエストを作成する

github.com や GitHub コマンドラインインターフェイス (CLI) など、PR を作成する方法はいくつかあります。GitHub Copilot を使っているので、PR の作成も依頼しましょう。関連する Issue を探し、関連付けて PR を作成できます。

1. Copilot Chat パネルに移動し、**New Chat** を選択して新しいセッションを開始します。
2. Copilot が GitHub ツールを使えるよう、エージェント一覧で **Agent** が選択されていることを確認します。
3. 次のプロンプトで PR の作成を依頼します。

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. 必要に応じて **Continue** を選択し、情報の取得や操作を許可します。GitHub ツールの初回利用時に GitHub 認証を求められた場合は、画面の指示に従います。
5. Copilot が Issue を検索し、該当する Issue を見つけて PR を作成する様子を確認します。
6. Copilot が生成したリンクを選択して PR をレビューします。ただし、まだマージしないでください。

## まとめと次のステップ

この演習では、次の作業を行いました。

- Model Context Protocol (MCP) と、MCP サーバーで Copilot にツールを追加する方法を学びました。
- Playwright MCP サーバーをワークスペースに追加しました。
- 出荷前にブラウザーで絞り込み機能を手動テストしました。
- ブランチを公開し、絞り込み機能のプルリクエストを作成しました。

機能のテストに MCP サーバーを使用しましたが、MCP は Copilot を拡張する方法の 1 つです。次は、アクセシビリティレビューなど、対象を絞った作業を効率化する[カスタムエージェントを作成します][next-lesson]。

## リソース

- [MCP とは何か、なぜ話題になっているのか][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [GitHub MCP Server][github-mcp-server]
- [GitHub MCP Registry][mcp-registry]
- [VS Code の MCP サーバー][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
