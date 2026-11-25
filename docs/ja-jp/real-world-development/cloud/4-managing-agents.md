---
title: "レッスン 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前の2つの演習では、ユーザー体験の改善と機能追加を目的とする3つのタスクを Copilot cloud agent に依頼しました。cloud agent は非同期かつ自律的に作業しますが、タスクを監視することも大切です。

cloud agent に割り当てたタスクを管理する方法はいくつかあります。GitHub.com の[agents ページ][agents-page]では、オープンなプルリクエスト (PR) があるすべてのエージェントタスクを確認できます。エージェントが行った操作を確認し、進行中のセッションに指示を追加して作業を導くこともできます。

このレッスンでは、次のことを行います。

- agents ページから cloud agent のタスクを監視します。
- 進行中のセッションに機能追加を依頼します。

## シナリオ

ハイコントラストモードを作成するようエージェントに依頼した後、チームはライトモードも追加したいと考えました。サイトのスタイルを更新し、切り替え機能を追加しているところなので、合わせて実装するのが合理的です。ハイコントラストに加えてライトモードも追加されるよう、エージェントの作業を案内します。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てたタスクの現在の状態を確認しましょう。

1. [Copilot agents ページ](https://github.com/copilot/agents)に移動します。
2. メインペインと左ペインの両方に表示されるタスク一覧を確認します。Copilot に割り当てた、次のタスクなどが表示されます。
   - コードのドキュメントを更新する
   - ゲーム変更用の API を生成する
   - Web サイトにハイコントラストモードを追加する
3. 実行中のタスクを選択し、Copilot が行った操作を確認します。次のような操作が含まれます。
   - リポジトリのコードをチェックアウトする
   - Copilot の作業環境を作成する
   - MCP サーバーを設定する
   - 割り当てられたタスクを完了するために、さまざまな手順を実行する

> [!NOTE]
> 表示される手順は、Copilot の作業状況や採用した方法によって異なります。

4. 右側に表示されるプルリクエスト (PR) ペインも確認します。ここから PR と変更されたファイルを確認し、さらに詳しく監視できます。

## cloud agent の作業を案内する

実行中のタスクを確認できたので、ハイコントラストモードの作業中にライトモードの切り替えも追加するよう Copilot に依頼します。

1. ハイコントラストモードの追加に関するセッションを選択します。表示されるタイトルは Copilot が付けた名前や作業状況によって異なります。

   ![mission control のアクセシビリティセッション](../../../_images/ex6-accessibility-session.png)

2. セッションを数分間確認し、セットアップが完了して作業を始めたことを確認します。次のようなメッセージが表示されたら、作業を開始しています。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを入力します。

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![Copilot が作業中のセッションに追加指示を送るダイアログが強調表示された agents ページの画面](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot がプロンプトを受け取り、作業手順に加えることを確認します。

## Copilot に作業を続けさせる

前回と同じように、Copilot は更新されたタスクに取り組みます。メッセージを送信した時点で作業中だった手順を完了した後、新しい依頼を作業に取り入れます。

今回も数分かかります。その間に、ここまでに学んだことを振り返りましょう。

## まとめと次のステップ

このレッスンでは、GitHub Copilot cloud agent のタスクを監視して案内する中心的な場所である Copilot agents ページを確認しました。mission control から実行中と完了済みのタスクを追跡し、実行された作業を確認し、進行中のタスクに新しい指示を追加できます。

このレッスンでは、次のことを行いました。

- mission control と agents ページから cloud agent のタスクを監視しました。
- 進行中のセッションに機能追加を依頼しました。

Copilot がアクセシビリティ機能を実装している間に、次は[Copilot が作成したプルリクエストを繰り返し改善します][next-lesson]。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタムエージェントについて][custom-agents]

---

| [← 前のレッスン: カスタムエージェント][previous-lesson] | [次のレッスン: Copilot の作業を繰り返し改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
