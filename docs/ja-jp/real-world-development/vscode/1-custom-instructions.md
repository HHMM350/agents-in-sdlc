---
title: "演習 1 - カスタム指示 (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: エージェントモード →][next-lesson]

生成 AI を使う際、コンテキストが重要です。特定の方法で作業する必要がある場合や、Copilot に背景情報を伝えたい場合は、そのコンテキストを参照できるようにします。コード生成の指針を伝える方法の 1 つが[指示ファイル][instruction-files]です。

この演習では、次の作業を行います。

- リポジトリのカスタム指示とパスで対象を指定した指示ファイルを使い、プロジェクト固有のコンテキスト、コーディングガイドライン、ドキュメント標準を Copilot に伝える方法を確認します。
- 既存の指示に従って、絞り込み機能の最初のデータ部分となる publisher ヘルパーを生成します。
- リポジトリ全体に適用する標準を `.github/copilot-instructions.md` に追加します。
- 同じプロンプトを再実行し、生成コードが新しい標準に従うことを確認します。
- 次の演習で新しい指示を活用できるよう、指示と絞り込み機能の一部を `main` にコミットします。

> [!CAUTION]
> 生成コードが設定した標準から外れる場合があります。Copilot の動作は確率的です。この演習では、指示を更新した後の動作の**傾向**を確認します。生成結果が文字単位で同じになることは想定しません。

## 指示ファイル

### シナリオ

Tailspin Toys には、開発プロセスに関するガイドラインと要件があります。たとえば、次のようなものです。

- データ層には必ずユニットテストを用意します。
- UI はダークモードにし、現代的な見た目にします。
- TSDoc のドキュメントコメントをコードに追加します。
- 各ファイルの先頭に、そのファイルの役割を説明するコメントブロックを追加します。

指示ファイルを使って、Copilot がこれらの開発手法に沿って作業できるようにします。

### カスタム指示

カスタム指示を使うと、コーディングスタイルや要件を Copilot に伝え、より適切な提案やコードを生成するようにガイドできます。コーディング規約、ライブラリ、コードに含めるコメントの種類などを指定できます。リポジトリ全体、または特定のファイル種類に対するタスク単位の指示を作成できます。

指示ファイルには次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリに関する**すべての**リクエストで Copilot に送信される単一の指示ファイルです。技術スタック、開発内容の概要、ベストプラクティスなど、プロジェクト全体の情報を記載します。
- `.github/instructions/*.instructions.md` ファイルには、特定の作業やファイルの種類に関する指示を記載します。TypeScript や Astro などの言語、UI コンポーネントの作成、新しいテストの作成などが対象です。

> [!NOTE]
> IDE では、指示ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、コード生成時にリポジトリレベルの指示と `applyTo` frontmatter を含む `*.instructions.md` ファイルの両方を使います。
>
> Copilot は AGENTS.md や CLAUDE.md など、別の標準で作成された指示ファイルにも対応しています。詳細は[カスタム指示のサポート][custom-instructions-support]を参照してください。

### 指示ファイルを管理するためのベストプラクティス

指示ファイルの作成方法をすべて説明することは、このワークショップの範囲外です。サンプルプロジェクトでは代表的な方法を紹介しています。基本的には、次の点を意識してください。

- `copilot-instructions.md` には、開発内容、プロジェクト構成、全体に適用されるコーディング標準など、プロジェクトレベルのガイダンスを記載します。
- `*.instructions.md` は、ユニットテスト、Astro コンポーネント、データ層などのファイル種類や、特定の作業に関する指示に使います。
- 自然な言葉で、明確なガイダンスを記載します。望ましいコードと避けるべきコードの例も示します。

指示ファイルの作成方法や AI の使い方に唯一の正解はありません。プロジェクトに合った方法を試しながら見つけてください。

> [!TIP]
> GitHub Copilot を使うプロジェクトでは、指示ファイルを充実させることをお勧めします。このプロジェクトには、[UI の更新][ui-instructions]や [Astro][astro-instructions] など、多くの作業向けのファイルがあります。
>
> Copilot に指示ファイルを生成させることもできます。VS Code の **Configure Chat → Generate Agent Instructions** や Copilot CLI の `/init` など、利用環境によって方法が異なります。このワークショップでは、該当する場合に説明します。
>
> テンプレートや開始点を探している場合は、指示ファイルやカスタムエージェントなどのリソースをまとめた [awesome-copilot][awesome-copilot] を確認してください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム指示ファイルを確認する

このリポジトリに含まれる指示ファイルを確認します。基本となる `copilot-instructions.md` と、さまざまな作業向けの `*.instructions.md` ファイルがあります。エディターまたは GitHub Web UI で開いてください。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの簡潔な説明や、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** の下には **GitHub Actions Workflows** の指針もあります。これらは Copilot とのあらゆるやり取りに適用されます。
3. `.github/instructions` フォルダーを開いて内容を確認します。Astro ファイル、Drizzle データ層、テストなどの指示があります。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドには、指示の対象ファイルを決める、リポジトリルートからの glob が設定されています。ここでは、`**/*.test.ts` に一致する TypeScript のテストファイルが対象です。
5. このプロジェクトでユニットテストを作成する際の指示を確認します。
6. `.github/instructions/drizzle.instructions.md` を開き、末尾までスクロールします。`unit-tests.instructions.md` などの指示ファイルや、プロジェクトの既存ファイルへのリンクを確認します。大きな指示を再利用可能な小さなファイルに分け、コード生成時に参照する例を示せます。ここに記載されたパスは指示ファイルからの相対パスです。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはプロジェクトのコーディング標準が記載されていますが、コード内のドキュメントに関する要件はまだありません。次の手順で TSDoc コメントとファイルヘッダーのルールを追加します。

## 変更用ブランチを作成する

ベストプラクティスに従い、変更用のブランチを作成します。

1. 前の演習で使った Codespace に戻ります。
2. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して新しいターミナルを開きます。
3. 新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions
   ```

## 指示を更新する前に Copilot Chat を使う

> [!TIP]
> **Copilot Chat を開く**
>
> 以下の演習を始める前に Codespace に戻り、Copilot Chat パネルを開いて **New Chat** を選択し、新しい会話を始めてください。モードとモデルの選択は演習によって異なります。必要な場合は各手順で説明します。

カスタム指示の効果を確認するため、まず現在の指示ファイルを使ってプロンプトを送信します。後で指示を更新して、同じプロンプトを再送信し、違いを確認します。

1. 前の演習から開いているエディタータブを閉じ、Copilot が必要なコンテキストだけを使うようにします。
2. `src/lib/publishers.ts` を開き、ヘルパーを作成する場所を Copilot に示します。
3. Chat ビューのエージェント一覧で **Agent** を選択し、Copilot がファイルを変更できるようにします。

   ![Chat ビューのエージェント選択メニューのスクリーンショット。](../../../_images/shared-chat-mode-selector.png)

4. 次のプロンプトを送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot はプロジェクトを調べてコードを更新します。多くの場合、ヘルパーファイルとテストが変更されます。
6. 提案されたヘルパーが、`db` クライアントを最初の引数として受け取り、publisher の型付き配列を返す関数であることを確認します。これは `src/lib/*.ts` に適用される `.github/instructions/drizzle.instructions.md` の規約に基づいています。
7. 提案されたコードに TSDoc コメントとファイルレベルのコメントヘッダーが**ない**ことを確認します。

> [!CAUTION]
> Copilot の動作は確率的なため、指示がなくてもドキュメントコメントを追加する場合があります。その場合も問題ありません。指示を更新した後に動作が一貫することが、この演習の目的です。

## リポジトリ全体の標準を追加する

`.github/copilot-instructions.md` は Copilot にプロジェクトレベルの情報を提供します。コードの提案を改善するため、リポジトリのコーディング標準を記載しましょう。

1. `.github/copilot-instructions.md` をもう一度開きます。
2. 27 行目付近にある **Code formatting requirements** セクションを見つけます。既存の標準にはコード内のドキュメントについてのルールがありません。
3. 既存の標準の直下に次の Markdown を追加し、ファイルヘッダーと TSDoc コメントを追加するよう Copilot に指示します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 前のレッスンで確認したように、指示ファイルはリポジトリレベル (`.github/copilot-instructions.md`) に作成して全体に適用したり、特定の言語、ファイル種類、作業向けの `*.instructions.md` ファイルとして作成したりできます。追加したドキュメントコメントのルールのようにプロジェクト全体に適用する標準は、リポジトリレベルのファイルに記載します。

## プロンプトを再実行して変化を確認する

1. Copilot Chat に戻り、**New Chat** を選択して会話を新しくします。
2. `src/lib/publishers.ts` をもう一度開き、Copilot が適切なファイルを参照するようにします。
3. 前と**同じプロンプト**を送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 提案されたファイルの先頭に、次のようなコメントブロックが追加されていることを確認します。

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. 提案された関数に次のような TSDoc コメントが含まれることを確認します。

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

新しいプロジェクト標準に従うよう Copilot をガイドし、次の演習で使うコードに適用できました。

## 指示とブランチをコミットしてプッシュする

指示ファイルもリポジトリ内の他のファイルと同じようにソース管理します。変更をコミットしてブランチをリポジトリにプッシュしましょう。

1. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して新しいターミナルを開きます。
2. 次のコマンドを実行し、指示の更新とヘルパーの変更を確認します。

   ```bash
   git status
   ```

3. 指示の変更と、ヘルパーの基礎作成に関係して Copilot が変更したファイルをステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # git status にテストなどの追加変更が表示された場合は、それらのファイルも追加します。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. ブランチをリポジトリにプッシュします。

   ```bash
   git push -u origin custom-instructions
   ```

## プルリクエストを作成してマージする

ブランチをプッシュしたら、バックログのドキュメント標準に関する Issue に関連付けてプルリクエストを作成します。GitHub ツールはすでにプロジェクトに接続されているため、Copilot に Issue を見つけて、Issue をクローズする PR を作成し、マージするよう依頼できます。

> [!NOTE]
> この演習では、Copilot が初めて GitHub 上で操作します。プロジェクトのテンプレートには GitHub ツールがすでに設定されています。最初の使用時に VS Code から GitHub へのサインインを求められた場合は、指示に従って許可してください。接続の仕組み (Model Context Protocol) は後の演習で学びます。

1. Codespace で Copilot Chat を開きます。
2. <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) を押して Copilot Chat ビューを開き、エージェント一覧で **Agent** が選択されていることを確認します。
3. 指示ファイルを更新する Issue を見つけ、現在のブランチから PR を作成するよう Copilot に依頼します。指示の更新と、今後の絞り込み機能で使う publisher ヘルパーの基礎作成を説明に含めます。

   ```
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot が Issue を探して PR を作成します。
5. GitHub 操作の **Allow** を求められたら、コマンドを確認して適切な場合に選択します。
6. PR が作成されたら、次のプロンプトでマージしてローカルブランチを `main` に戻すよう依頼します。

   ```
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. GitHub 操作やシェルコマンドの **Allow** を求められた場合は、内容を確認して適切な場合に許可します。

GitHub Copilot の支援でプルリクエストを作成してマージできました。

## まとめと次のステップ

このプロジェクトで Copilot が指示ファイルからコンテキストを取得する方法を確認し、VS Code の Copilot Chat を使って次の作業を行いました。

- コード生成プロンプトを送信し、**既存の**指示で Copilot が生成する内容を確認しました。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加しました。
- 同じプロンプトを再送信し、新しい標準に従うコードを確認しました。
- 次の演習で利用できるよう、指示とヘルパーの基礎作成を `main` にコミットしました。

次は[エージェントモード][next-lesson]を使い、コードベース全体にわたる新機能を Copilot に追加させます。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベストプラクティス][instructions-best-practices]
- [Copilot のカスタム指示を改善する 5 つのヒント][copilot-instructions-five-tips]
- [GitHub Copilot の個人用カスタム指示][personal-instructions]
- [Awesome Copilot — 指示ファイルなどのリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
