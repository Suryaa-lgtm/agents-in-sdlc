---
title: "レッスン 10 - まとめと次のステップ"
description: "Copilot CLI のワークフロー、2つのプルリクエスト、再利用可能なカスタマイズ、追加リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Tailspin Toys の一連の開発ワークフローで GitHub Copilot CLI を使いました。次のことを行いました。

- Codespace を準備し、Copilot CLI をインストールして、プロジェクトを確認し、事前に登録されたフィルタリング issue を見つけました。
- 星評価を追加し、転送されたブラウザーで結果を確認して、最初のプルリクエスト (PR) を手動でマージしました。
- フィルタリング issue を起点に Plan モードで進め方を決め、Autopilot モードで実装し、Interactive モードでレビューしました。
- カスタム指示でエージェントを導き、既存の `quality-checks` スキルをカスタマイズして、ユニットテスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーでフィルタリングを試しました。
- QA カスタムエージェントを作成して選択し、要件、カバレッジ、スキルの結果、ブラウザーでの証拠を確認しました。
- フィルタリングの変更全体をレビューし、フィルタリング PR に Agent Merge を許可しました。
- コンテキスト、モデル、共有、省略可能なクラウドへの委任に使うスラッシュコマンドを確認しました。

## リリースした内容

ワークショップでは、更新済みの `main` から個別のブランチを作り、2つの PR を作成しました。

1. **星評価:** 既存の `starRating` と未評価状態をゲームカードに表示します。
2. **フィルタリングと品質ワークフロー:** フィルタリングを実装し、指示を更新して機能に適用し、`quality-checks` のレポートをカスタマイズし、QA プロファイルと関連テストを追加します。

フィルタリングの計画から PR 作成まで、同じ会話とブランチを使いました。ワークショップを簡潔にするため、作業を1つの PR にまとめています。

## さまざまな検証方法

自動テスト、自分でのブラウザー確認、MCP を使った Copilot のブラウザー確認など、複数の方法でコードを確認しました。`quality-checks` スキルはユニットテスト、lint、型チェックを実行し、新しい形式で結果を報告しました。QA はこれらの結果と要件およびテストカバレッジのレビューをまとめ、PR 作成前の確認に役立てました。

追加するテストで実際の不足を解決する必要があります。QA を実行して新しいテストが不要と判断される場合もあります。マージを許可する前に、コードと根拠を確認し、変更後は影響する検証結果を更新してください。

## ベストプラクティス

Copilot に提供するコンテキストとツールが、作業の内容に影響します。このワークショップでは、指示を更新し、スキルをカスタマイズし、QA プロファイルを作成し、MCP サーバーを設定しました。会話をまたいでカスタマイズを再利用し、チームのニーズに合わせて調整できます。指示は標準を定め、スキルは繰り返し実行するタスクを記述し、カスタムエージェントは専門家の役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果を確認してください。

タスクに合った**モードとモデル**を選びます。**Plan** は実装前に進め方を考えるとき、**Interactive** は小さな変更を一緒に進めるとき、**Autopilot** は範囲が明確なタスクを任せるときに使います。定型的な編集には高速なモデルを、複雑な作業にはより高性能なモデルを選びます。

インフラストラクチャと同じくらい、コンテキストも重要です。作りたいもの、理由、実現方法を明確に説明すると、結果が大きく変わります。

## さらに試す

主要なワークフローを学びました。Copilot CLI のほかの機能も試してみましょう。

- `/review` でコードレビューエージェントに変更の分析を依頼します。
- `/rubber-duck` で問題を相談し、別の見方を得ます。
- `/fleet` で独立したサブタスクを並行して調整します。
- `/worktree` で別のタスクを分離します。
- `/delegate` でタスクを Copilot cloud agent に送信します。

## 次のステップ

どのツールも、使い続けることで上達します。実際のコード、趣味のコード、長い間作ろうと思っていた小さなアプリなどで活用してください。チームで学んだことを共有し、互いの経験から学びましょう。ドキュメントも引き続き確認してください。

ターミナルから Tailspin Toys を拡張したい場合は、省略可能な[Foundry Backer Concierge シリーズ][foundry]に進みます。ほかの環境での開発を比べるには、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、[Copilot cloud agent ワークショップ][cloud]を確認してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンドリファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
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
