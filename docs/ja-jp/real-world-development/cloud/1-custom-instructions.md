---
title: "演習 1 - カスタム指示 (Cloud agent)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を使う際、コンテキストが重要です。特定の方法で作業する必要がある場合や、Copilot が知っておくべき背景情報がある場合は、そのコンテキストにアクセスできるようにします。[指示ファイル][instruction-files]を使うと、Copilot に何をしてほしいかだけでなく、どのように作業してほしいかも伝えられます。

この演習では、次の作業を行います。

- リポジトリのカスタム指示とパスで対象を指定した指示ファイルを使い、プロジェクト固有のコンテキスト、コーディングガイドライン、ドキュメント標準を Copilot に伝える方法を確認します。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加します。

> [!NOTE]
> VS Code や CLI のハーネスとは異なり、この演習では変更前後のプロンプトを比較しません。Copilot cloud agent は GitHub Issue に対して非同期で作業するため、リアルタイムで並べて効果を示すのが難しいためです。後続の演習で cloud agent が作成するプルリクエストをレビューする際に、指示ファイルの影響を確認します。

## 指示ファイル

### シナリオ

Tailspin Toys には、開発プロセスに関するガイドラインと要件があります。たとえば、次のようなものです。

- データ層には必ずユニットテストを用意します。
- UI はダークモードにし、現代的な見た目にします。
- TSDoc のドキュメントコメントをコードに追加します。
- 各ファイルの先頭に、そのファイルの役割を説明するコメントブロックを追加します。

指示ファイルを使って、Copilot がこれらの開発手法に沿って作業できるよう、適切な情報を提供します。

### カスタム指示

カスタム指示を使うと、Copilot がコーディングスタイルや要件を理解できるよう、コンテキストや設定を伝えられます。希望するコーディング規約、ライブラリ、コードに含めるコメントの種類などを指定して、より適切な提案やコードを生成するようにガイドできます。リポジトリ全体、または特定の種類のファイルに対するタスク単位の指示を作成できます。

指示ファイルには次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリに関する**すべての**リクエストで Copilot に送信される単一の指示ファイルです。Copilot Chat や CLI から送る多くのリクエストに関係する技術スタック、開発内容の概要、ベストプラクティスなど、プロジェクト全体の情報を記載します。
- `.github/instructions/*.instructions.md` ファイルは、特定の作業やファイルの種類に合わせて作成できます。TypeScript や Astro などの言語、UI コンポーネントの作成、新しいテストの作成といった作業向けのガイドラインを記載します。

> [!NOTE]
> IDE では、指示ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、コード生成時にリポジトリレベルの指示と `applyTo` frontmatter を含む `*.instructions.md` ファイルの両方を使用します。
>
> Copilot は AGENTS.md や CLAUDE.md など、別の標準で作成された指示ファイルにも対応しています。詳細は[指示ファイルのサポート][custom-instructions-support]を参照してください。

### 指示ファイルを管理するためのベストプラクティス

指示ファイルの作成方法をすべて説明することは、このワークショップの範囲外です。ただし、サンプルプロジェクトでは代表的な方法を紹介しています。基本的には、次の点を意識してください。

- `copilot-instructions.md` には、開発内容、プロジェクト構成、全体に適用されるコーディング標準など、プロジェクトレベルのガイダンスを記載します。
- `*.instructions.md` は、ユニットテスト、Astro コンポーネント、データ層などのファイル種類や、特定の作業に関する指示に使います。
- 自然な言葉で、明確なガイダンスを記載します。望ましいコードと避けるべきコードの例も示します。

指示ファイルの作成方法や AI の使い方に唯一の正解はありません。プロジェクトに合った方法を試しながら見つけてください。

> [!TIP]
> GitHub Copilot を使うすべてのプロジェクトで、指示ファイルを充実させることをお勧めします。このプロジェクトには、[UI の更新][ui-instructions]や [Astro][astro-instructions] など、多くの作業向けのファイルがあります。
>
> Copilot に指示ファイルを生成させることもできます。VS Code の **Configure Chat → Generate Agent Instructions** や Copilot CLI の `/init` など、Copilot の利用環境によって方法が異なります。このワークショップでは、該当する場合に利用環境ごとの方法を説明します。
>
> テンプレートや開始点を探している場合は、指示ファイルやカスタムエージェントなどのリソースをまとめた [awesome-copilot][awesome-copilot] を確認してください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム指示ファイルを確認する

このリポジトリに含まれる指示ファイルを確認します。基本となる `copilot-instructions.md` と、さまざまな作業向けの `*.instructions.md` ファイルがあります。エディターまたは GitHub の Web UI で開いてください。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの簡潔な説明や、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** の下には **GitHub Actions Workflows** の指針があります。これらは Copilot とのあらゆるやり取りに適用されます。
3. `.github/instructions` フォルダーを開いて内容を確認します。Astro ファイル、Drizzle データ層、テストなどの指示があります。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドには、指示を適用するファイルを決める、リポジトリルートからの glob が設定されています。ここでは、`**/*.test.ts` に一致する TypeScript のテストファイルが対象です。
5. このプロジェクトでユニットテストを作成する際の指示を確認します。
6. 最後に `.github/instructions/drizzle.instructions.md` を開き、末尾までスクロールします。`unit-tests.instructions.md` などの指示ファイルや、プロジェクト内の既存ファイルへのリンクを確認します。このように大きな指示を再利用可能な小さなファイルに分け、コード生成時に参照する例を示せます。ここに記載されたパスはリポジトリルートではなく、指示ファイルからの相対パスです。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはプロジェクトのコーディング標準が記載されていますが、コード内のドキュメントに関する要件はまだありません。次の手順で TSDoc コメントとファイルヘッダーのルールを追加します。

## リポジトリ全体に適用する標準を追加する

この演習で編集するのは、プロジェクト全体に適用するルールの追加だけです。コード内のドキュメントは TSDoc コメントとファイルレベルのコメントヘッダーで記述するよう標準に加えます。後続の演習で Issue を割り当てると、cloud agent はこの指示に従います。

編集の前にブランチを作成します。cloud agent は Issue の対象ブランチにある指示を読み取りますが、ここでは変更をきちんとコミットします。

1. Codespace のターミナルで新しいブランチを作成し、切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

前述のとおり、`.github/copilot-instructions.md` はプロジェクトレベルの情報を Copilot に提供します。コードの提案を改善するため、リポジトリのコーディング標準を記載します。

1. `.github/copilot-instructions.md` をもう一度開きます。
2. 27 行目付近にある **Code formatting requirements** セクションを見つけます。プロジェクトのコーディング標準が記載されていますが、生成されたヘルパーにドキュメントコメントがなかった理由となる、コード内のドキュメントに関するルールはまだありません。
3. 既存の標準の直下に次の Markdown を追加し、ファイルヘッダーと TSDoc ドキュメントコメントを追加するよう Copilot に指示します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 前のレッスンで確認したように、指示ファイルはリポジトリレベル (`.github/copilot-instructions.md`) に作成して全体に適用したり、特定の言語、ファイル種類、作業向けの `*.instructions.md` ファイルとして作成したりできます。追加したドキュメントコメントのルールのようにプロジェクト全体に適用する標準は、リポジトリレベルのファイルに記載します。

## 指示の変更をコミット、プッシュ、マージする

Cloud agent は、Issue の対象ブランチにある指示ファイルを読み取ります。次の演習で Issue を Copilot に割り当てると、Copilot は `main` からブランチを作成します。そのため、cloud agent が新しい指示を読み取れるよう、変更を `main` に取り込む必要があります。

1. 変更をステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` へのプルリクエストを作成してマージします。次の演習で Issue に割り当てると、cloud agent はこの指示を読み取ります。

> [!TIP]
> このワークショップでは、ブランチを使わず `main` に直接作業してもかまいません。実際のプロジェクトでの手順を体験できるよう、ここではブランチを作成しています。

## まとめと次のステップ

このプロジェクトで Copilot が指示ファイルからコンテキストを取得する方法を確認し、`.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加しました。残りのハーネスで cloud agent が作成するプルリクエストをレビューし、この標準が適用されていることを確認します。

次は [Copilot cloud agent に最初の Issue を割り当て][next-lesson]ます。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベストプラクティス][instructions-best-practices]
- [Copilot のカスタム指示を改善する 5 つのヒント][copilot-instructions-five-tips]
- [Awesome Copilot — 指示ファイルなどのリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
