---
title: "レッスン 4 - カスタム指示で Copilot をガイドする"
description: "リポジトリの指示を確認し、ドキュメントの標準を追加して、絞り込み機能のコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を使う際、コンテキストが重要です。特定の方法で作業する必要がある場合は、Copilot がそのガイダンスを参照できるようにします。[指示ファイル][instruction-files]では、求めるコードだけでなく、その構造や記述方法も伝えられます。絞り込み機能を実装したので、Copilot が使用した指示を確認し、ドキュメントの標準を追加して、コードに適用します。

このレッスンでは、次の作業を行います。

- リポジトリの指示とパスで対象を指定した指示ファイルがエージェントに適用される方法を確認します。
- コーディング標準を適用するために指示ファイルを更新します。
- 指示ファイルがコードに与える影響を確認します。

## シナリオ

Tailspin Toys には、開発プロセスに関するガイドラインと要件があります。たとえば、次のようなものです。

- コメントでは、コードの内容を言い換えるのではなく、意図と自明でない判断を説明します。
- `db/` と `src/lib/` にあるエクスポートされた関数では、`db` の注入可能な引数がある場合はそれも含めて、目的、パラメーター、戻り値を TSDoc/JSDoc で説明します。
- 再利用可能な Astro コンポーネントでは `Props` の契約を説明し、関連するコードの変更時にコメントを最新の状態に保ちます。
- 既存のフォーマットと lint の指針を維持します。

指示ファイルを使って、Copilot がこれらの開発手法に沿って作業できるよう、適切な情報を提供します。

## 指示ファイル

カスタム指示を使うと、Copilot がコーディングスタイルや要件を理解できるよう、コンテキストや設定を伝えられます。希望するコーディング規約、ライブラリ、コードに含めるコメントの種類などを指定して、より適切な提案やコードを生成するようにガイドできます。リポジトリ全体、または特定のファイルや作業に対する指示を作成できます。

指示ファイルには次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリに関する**すべての**リクエストで Copilot に送信される単一の指示ファイルです。多くのリクエストに関係するプロジェクトレベルの情報を記載します。
- `.github/instructions/*.instructions.md` ファイルには、特定の言語、ファイル種類、作業に関するガイドラインを記載します。

> [!NOTE]
> その他の指示形式やサポート状況は、利用環境によって異なります。特定の形式に依存する前に、[カスタム指示のサポートに関するリファレンス][custom-instructions-support]を確認してください。

## このプロジェクトのカスタム指示ファイルを確認する

スタータープロジェクトには、すでに複数の指示ファイルが含まれています。変更を加える前に、ファイルを確認して影響を把握しましょう。

1. Codespace に戻ります。
2. Codespaces のエディターで (ターミナルではなく) `.github/copilot-instructions.md` を開きます。
3. プロジェクトの簡潔な説明とコーディングガイダンスを確認します。このリポジトリでの Copilot とのすべてのやり取りに適用されます。
4. `.github/instructions` フォルダーを開き、ファイルを確認します。Astro ファイル、Drizzle データ層、テストなどの指示があります。
5. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドには、指示の対象ファイルを決める glob が設定されています。
6. `.github/instructions/drizzle.instructions.md` を開き、ほかの指示ファイルやプロジェクトの既存ファイルへのリンクを確認します。指示を再利用しやすい小さなファイルに分け、Copilot が参考にできる例を示せます。

## チームのガイダンスに合わせて指示ファイルを更新する

既存のファイルはよい開始点ですが、まだ改善できます。コアの `copilot-instructions.md` ファイルを編集し、新しく生成される TypeScript に TSDoc コメントを追加するよう指示します。

1. `.github/copilot-instructions.md` で、35 行目付近にある **Code formatting guidance** セクションを見つけます。
2. 最後の箇条書きに次の内容を追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

ファイルは自動的に保存されます。

## 更新したガイダンスを使う

Copilot CLI は会話の開始時にリポジトリの指示を読み込みます。指示を更新した後、会話を終了して絞り込みの会話を再開すると、機能のコンテキストを保持したまま新しいガイダンスを読み込めます。

1. 絞り込みの会話が開いている場合は、`/exit` を入力して閉じます。Copilot CLI は会話を自動的に保存します。
2. リポジトリのルートにある `game-filters-cli` ブランチから、保存した会話を再開します。

   ```bash
   copilot --resume
   ```

   プロンプトが表示されたら、絞り込みの会話を選択し、`game-filters-cli` ブランチがチェックアウトされていることを確認します。
3. 更新したガイダンスを適用するよう Copilot に依頼します。

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. `/diff` を入力し、変更された TypeScript ファイルを確認します。新しい TSDoc コメントが追加され、コードを正確に説明していることを確認します。

## まとめと次のステップ

Copilot CLI が指示ファイルからコンテキストを取得する方法を確認し、機能に新しい標準を適用しました。このレッスンでは、次の作業を行いました。

- リポジトリの指示とパスで対象を指定した指示ファイルがエージェントに適用される方法を確認しました。
- コーディング標準を適用するために指示ファイルを更新しました。
- 指示ファイルがコードに与える影響を確認しました。

次は、再利用可能な quality-checks スキルを[カスタマイズして実行し][next-lesson]、lint とテストを一貫して実行します。

## リソース

- [Copilot CLI のカスタム指示の追加][instruction-files]
- [カスタム指示のサポート][custom-instructions-support]
- [カスタム指示を作成するためのベストプラクティス][instructions-best-practices]
- [Awesome Copilot — 指示ファイルなどのリソース集][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
