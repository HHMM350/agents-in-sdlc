---
title: "レッスン 5 - quality-checks スキルをカスタマイズして使う"
description: "既存の quality-checks スキルを確認し、レポート形式をカスタマイズして、絞り込み機能の検証に使います。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

コードを書くことだけが開発ではありません。手動でコードの動作を確認し、指示ファイルで標準に従わせました。テストや lint、継続的インテグレーション (CI) の他の作業はどうでしょうか。

こうした作業には**エージェントスキル**が適しています。スキルを使うと、これらの操作を正しく実行する方法を Copilot に伝えられます。

このレッスンでは、次の作業を行います。

- 既存の `quality-checks` スキルを確認します。
- 結果の形式をカスタマイズします。
- スキルを再読み込みして実行します。

## シナリオ

Tailspin Toys では、ユニットテスト、lint、型チェックに `quality-checks` スキルを使います。結果を読みやすくするため、レポートを改善したいと考えています。

## 指示、スクリプト、リソース

エージェントスキルには、再利用可能なタスクの指示、実行可能なスクリプト、エージェントが必要に応じて読み込む補助リソースをまとめられます。基本構成はスキル名のフォルダーと、その中の `SKILL.md` です。この Markdown ファイルには、スキルの名前と説明を定義する frontmatter、処理の概要、呼び出すタイミングのガイダンスを記載します。必要に応じて、スキルが呼び出すスクリプトや他のリソース用のサブフォルダーを追加できます。

> [!NOTE]
> スキルに追加のフォルダーやファイルは必須ではありません。Tailspin Toys の `quality-checks` スキルは、既存のプロジェクトコマンドを使うため、`SKILL.md` だけで構成されています。

スキルは、チームで共有して再利用できるリポジトリアセットとしてプロジェクトの `.github/skills` に置くことも、ユーザーのスキルフォルダー `~/.copilot/skills` に置くこともできます。

## スキルを確認する

Tailspin Toys チームがユニットテスト、lint、型チェックに使う `quality-checks` スキルを確認しましょう。

1. Codespace に戻り、Codespaces エディターで `.github/skills/quality-checks/SKILL.md` を開きます。
2. 先頭の `name` と `description` を読みます。説明は Copilot がスキルを呼び出すタイミングを判断するのに役立ちます。
3. 指示を読み、テストと lint の手順をどのようにガイドしているか確認します。
4. スキルには、まだ **Results output formatting** セクションがないことを確認します。

## 変更前にスキルを実行する

Copilot CLI から直接、または自然言語を使ってスキルを呼び出せます。Copilot に 3 種類のチェックを実行するよう依頼します。

1. 絞り込み機能の Interactive モードの会話に戻ります。
2. 次のプロンプトを送信します。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 完了時のレポートを確認します。

## レポートをカスタマイズする

どのチェックを実行したか、成功したか、ツールが実際に報告した内容がわかるよう、レポートを改善しましょう。

1. `.github/skills/quality-checks/SKILL.md` に戻ります。
2. ファイルの最後に次のセクションを追加します。

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. ファイルは自動的に保存されます。

## 更新したスキルを実行する

変更したスキルを Copilot CLI で使い、動作を確認しましょう。Copilot CLI は会話を再起動せずに、編集されたスキルを再読み込みできます。

1. 次のコマンドを入力します。

   ```plaintext
   /skills reload
   ```

2. 前とまったく同じプロンプトを送信します。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 最後のレポートを確認し、最初のレポートと比較します。

## まとめと次のステップ

既存のエージェントスキルをカスタマイズして使いました。このレッスンでは、次の作業を行いました。

- ユニットテスト、lint、型チェック用の `quality-checks` スキルを確認しました。
- 結果の形式をカスタマイズしました。
- スキルを再読み込みして実行しました。

この変更は絞り込み機能の PR に含めます。次は [Playwright MCP サーバー][next-lesson]を使って、Copilot がサイトを直接操作できるようにします。

## スキルの例

コミュニティの次の例は参考資料です。追加の作業項目ではありません。

- [Agent Skills 仕様][skill-spec]
- [コントリビューションのワークフロー: `make-repo-contribution`][contribution-example]
- [要件ドキュメント: `prd`][prd-example]
- [図とエクスポートスクリプトを含む `drawio`][drawio-example]
- [ブラウザーテスト: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
