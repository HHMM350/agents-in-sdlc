---
title: "演習 3 - カスタムエージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタムエージェントとは

GitHub Copilot の[カスタムエージェント][custom-agents-concept]を使うと、開発ワークフローの特定の作業や分野に合わせた AI アシスタントを作成できます。リポジトリの `.github/agents` フォルダーに Markdown ファイルを作成し、重点を絞った指示、ベストプラクティス、コーディングパターン、分野固有の知識を定義すると、特定の作業をより効果的に実行できるよう Copilot をガイドできます。チームの専門知識を再利用可能なエージェントにまとめることもできます。たとえば、[WCAG][wcag] 準拠を確認するアクセシビリティエージェント、安全なコーディングを支援するセキュリティエージェント、一貫したテストパターンを守るテストエージェントを作成できます。

カスタムエージェントは、プロジェクト内の `.github/agents` フォルダー、またはグローバルな `~/.copilot/agents` フォルダーにある Markdown ファイルで定義します。各ファイルには、少なくとも `name` と `description` を含む YAML frontmatter と、エージェントの動作、専門知識、指示を定義する Markdown プロンプトが必要です。

### カスタムエージェントとエージェントスキルの違い

カスタムエージェントと[エージェントスキル][agent-skills-concept]には、役割の重なる部分があります。どちらも主に Markdown ファイルで定義され、AI に作業方法を伝えます。わかりやすく区別するなら、**カスタムエージェントは作業者、スキルはツール**です。

カスタムエージェントには独自のコンテキストウィンドウがあり、作業の一部としてスキルや他のエージェントを調整できます。このラボのアクセシビリティカスタムエージェントは、アクセシビリティガイドラインに沿ってサイトをレビューし、更新します。その作業の一環として、プルリクエストのワークフローやテストの実行・管理を行うスキルを呼び出すこともできます。

> [!NOTE]
> カスタムエージェントの作成に唯一の正解はありません。AI の他の機能と同様に、環境やシナリオに合わせて試し、改善してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

カスタムエージェントでは、次の内容を学びます。

- カスタムエージェントの定義方法。
- カスタムエージェントへのタスクの割り当て方。

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず、すべてのユーザーがクラウドファンディングプラットフォームを使えるようにしたいと考えています。最近のユーザーフィードバックでは、テキストと背景色のコントラストが不十分なため、現在のダークテーマが読みにくいという意見が寄せられました。このアクセシビリティの課題に対応するため、デザインチームはユーザーが切り替えられるハイコントラストモードの実装を依頼しました。

アクセシビリティは重要なため、できるだけ早く実装する必要があります。カスタムエージェントを使って機能を実装します。

## アクセシビリティカスタムエージェントをレビューする

アクセシビリティ用のカスタムエージェントはすでに用意されています。内容をレビューして、Copilot をどのようにガイドするかを確認しましょう。

Codespace に戻り、アクセシビリティカスタムエージェントのファイルを確認します。

1. `.github/agents/accessibility.md` を開きます。
2. `name` フィールドと `description` フィールドを含む YAML frontmatter を確認します。

> [!CAUTION]
> カスタムエージェントには、`name` と `description` を含む frontmatter が必要です。

3. 続くセクションを確認します。アクセシブルな Web サイトのコード生成に関する主要な責任、アクセシビリティのベストプラクティス、HTML・CSS・JavaScript のコード例、よくある落とし穴や間違いが説明されています。

## Issue を作成して割り当てる

Mission control は、環境内のすべてのエージェントを操作するための中心的な場所です。Copilot cloud agent にタスクを割り当て、監視し、作業を方向付けたり追加のガイダンスを提供したりできます。まず、ハイコントラストモードの作成を Copilot に割り当てましょう。

1. リポジトリに移動します。
2. **Issues** タブを選択します。
3. **New issue** を選択して新しい Issue のダイアログを開きます。
4. **Blank issue** を選択して Issue を作成します。
5. **Title** に `Add high contrast mode to website` と入力します。
6. **Description** に次の内容を入力します。

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

7. **Create** を選択して Issue を作成します。
8. 右側の **Assign to Copilot** を選択して割り当てダイアログを開きます。
9. カスタムエージェントの一覧から **Accessibility agent** を選択します。

    ![カスタムエージェントとアクセシビリティが強調表示された cloud agent の割り当て画面](../../../_images/ex5-select-custom-agent.png)

10. **Assign** を選択します。
11. Copilot がバックグラウンドで作業を始めます。

## まとめと次のステップ

このレッスンでは、特定の作業や分野に合わせた AI アシスタントである [GitHub Copilot のカスタムエージェント][custom-agents]を学びました。カスタムエージェントにチームの専門知識と標準をまとめ、Copilot が作業をより効果的に実行できるようガイドできます。

次の内容を学びました。

- カスタムエージェントの定義方法。
- カスタムエージェントへのタスクの割り当て方。

Copilot がハイコントラストモードを実装している間に、次は Mission control から[エージェントセッションを監視して方向付けます][next-lesson]。

## リソース

- [カスタムエージェントについて][custom-agents]
- [Organization でカスタムエージェントを使うための準備][org-custom-agents]
- [Enterprise でカスタムエージェントを使うための準備][enterprise-custom-agents]

---

| [← 前のレッスン: GitHub Copilot cloud agent][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
