---
title: "レッスン 10 - まとめと次のステップ"
description: "Copilot CLI のワークフロー、2 件のプルリクエスト、再利用可能なカスタマイズ、その他のリソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Tailspin Toys で一連の作業を行い、GitHub Copilot CLI を活用しました。

- Codespace を準備し、Copilot CLI をインストールしてプロジェクトを確認し、用意されている絞り込みの Issue を見つけました。
- 星評価を追加し、転送ブラウザーで結果を確認して、最初のプルリクエスト (PR) を手動でマージしました。
- 絞り込みの Issue を起点に、Plan モードで方針を決め、Autopilot モードで実装して、Interactive モードでレビューしました。
- カスタム指示でエージェントをガイドし、既存の `quality-checks` スキルをカスタマイズして、ユニットテスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーで絞り込み機能を確認しました。
- quality assurance (QA) カスタムエージェントを作成・選択し、要件、テスト範囲、スキルの結果、ブラウザーの検証結果を評価しました。
- 絞り込みの変更全体をレビューし、絞り込みの PR で Agent Merge を承認しました。
- コンテキスト、モデル、共有、任意のクラウド委任に使うスラッシュコマンドを確認しました。

## 作成したもの

このワークショップでは、更新済みの `main` から個別のブランチを作り、2 つの PR を作成します。

1. **星評価**: 既存の `starRating` と、評価がないことを示す表示をゲームカードに追加します。
2. **絞り込みと品質のワークフロー**: 絞り込み機能を実装し、指示を更新してその機能に適用します。`quality-checks` のレポートをカスタマイズし、QA プロファイルを作成して、関連するテストを追加します。

絞り込み機能の計画から PR 作成まで、同じ会話とブランチを使いました。ワークショップを簡潔にするため、作業全体を 1 件の PR にまとめています。

## さまざまな検証方法

自動テスト、自分でのブラウザー確認、MCP を通じた Copilot のブラウザー操作など、複数の方法でコードを確認しました。`quality-checks` スキルではユニットテスト、lint、型チェックを実行し、新しい形式で報告しました。QA はその結果に、要件とテスト範囲のレビューをまとめました。

追加したテストで実際の不足が解消される必要があります。QA の実行時に新しいテストが不要でも、正しい場合があります。マージを承認する前にコードと検証結果をレビューし、変更後は影響する検証を再実行してください。

## ベストプラクティス

Copilot に与えるコンテキストとツールが、作業内容を左右します。このワークショップでは、指示を更新し、スキルをカスタマイズし、QA プロファイルを作成して、MCP サーバーを構成しました。これらのカスタマイズを複数の会話で再利用し、チームのニーズに合わせて調整できます。指示は標準を設定し、スキルは繰り返し実行する作業を説明し、カスタムエージェントは専門的な役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの概要だけではなく、実際の変更とツールの結果を確認してください。

タスクに合わせて**モードとモデル**を選択します。実装前に方針を検討するときは **Plan**、範囲を絞った変更に集中するときは **Interactive**、範囲が明確なタスクを任せるときは **Autopilot** を使います。定型的な編集には高速なモデルを選び、複雑な作業にはより高性能なモデルを選びます。

インフラストラクチャと同じくらいコンテキストも重要です。何を、なぜ、どのように実装するのかを明確に伝えると、出力が大きく変わります。

## さらに確認する

主要なワークフローを学びました。Copilot CLI には、次のような機能もあります。

- `/review` でコードレビューエージェントに変更を分析させます。
- `/rubber-duck` で問題を整理し、別の視点を得ます。
- `/fleet` で独立したサブタスクを並行して調整します。
- `/worktree` で別のタスクを隔離します。
- `/delegate` で Copilot cloud agent にタスクを送信します。

## 次のステップ

ツールの使い方を上達させるには、継続して使うことが大切です。本番コード、趣味のコード、何年も作りたいと思っていた小さなアプリなどで活用してください。チームで学びを共有し、互いの経験から学びましょう。ドキュメントも引き続き確認してください。

ターミナルから Tailspin Toys を拡張する場合は、任意の [Foundry Backer Concierge シリーズ][foundry]に進みます。他の環境で学ぶ場合は、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、[Copilot cloud agent ワークショップ][cloud]を確認してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI のカスタマイズ][customize-cli]
- [Copilot CLI でプルリクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
