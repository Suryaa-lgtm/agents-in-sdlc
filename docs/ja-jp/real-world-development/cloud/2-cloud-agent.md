---
title: "レッスン 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

技術的負債に悩んでいない組織は、ほとんどないでしょう。未解決のセキュリティ問題、更新が必要なレガシーコード、実装する時間がなくバックログに残った機能リクエストなどがあります。GitHub Copilot cloud agent は、コードの更新や機能の追加などのタスクを自律的に実行できます。エージェントは作業を終えると、開発者がレビューできるドラフト PR を作成します。面倒な作業を委任して開発を加速させ、開発者がより大きな課題に集中できるようになります。

このレッスンでは、Copilot cloud agent を使って次のことを学びます。

- コード生成の環境をカスタマイズします。
- 操作が安全に行われるようにします。
- 範囲を明確に定めた issue の重要性を理解します。
- issue を Copilot に割り当てます。

## シナリオ

Tailspin Toys には解決したい技術的負債があります。最初のサイトを開発した委託業者が、ドキュメントを適切に整備しませんでした。実際、ドキュメントはほとんどありません。まず、アプリケーションのすべてのエクスポート関数に TSDoc のドキュメントコメントを追加します。

また、デザインチームはゲームを見つけやすくしたいと考えています。各ゲームの詳細ページに、同じカテゴリに属する関連ゲームを表示し、閲覧を続けられるようにします。まだ完成度の高い実装は必要なく、UX の受け入れテストに使えるものを求めています。このタスクは現在ブロックされていますが、優先度の高い issue がほかにあります。

どちらも、優先順位が下がりやすいタスクの例です。Copilot cloud agent に割り当てれば、開発者は別の作業を続け、後から Copilot の作業をレビューできます。

## GitHub Copilot cloud agent とは

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) は、人間の開発者と同じように、バックグラウンドでタスクを実行できます。人間の開発者と同様に、作業方法はいくつかあります。その1つは、[GitHub issue を Copilot に割り当てる][assign-issue]方法です。割り当てると Copilot は進捗を記録するドラフトプルリクエストを作成し、環境をセットアップしてタスクに取り組みます。作業中でも完了後でも、Copilot のセッションを確認できます。提案された解決策のレビュー準備ができると、プルリクエストで通知されます。

## 範囲を明確にした指示の重要性

GitHub Copilot に魔法はありません。考える手間を省けるわけではありません。一見簡単そうな操作でも、詳しく見ると複雑なことがあります。[Copilot cloud agent に依頼するタスクの範囲に注意してください][cloud-agent-best-practices]。AI ペアプログラマーとして扱い、段階的に進めながら、学び、試し、調整してください。生成 AI を導入しても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム指示

前の演習では、カスタム指示とその効果を確認しました。カスタム指示の演習をすでに行った場合は `.github/copilot-instructions.md` を見たことがあるでしょう。まだの場合は、ここで少し確認してください。Copilot cloud agent に作業を割り当てる前に、このリポジトリに用意された指示ファイルを閲覧し、後からその影響を確認できるようにします。

リポジトリの GitHub Web UI、または起動済みの Codespace で次のファイルを開きます。

- `.github/copilot-instructions.md` — **Code standards** セクション、特に TypeScript の規約と TSDoc ドキュメントコメントの要件を確認します。
- `.github/instructions/unit-tests.instructions.md` — `applyTo` frontmatter を確認します。この指示は `**/*.test.ts` ファイルに適用されます。

次のセクションで `Code lacks documentation` issue を cloud agent に割り当てると、プルリクエストに TSDoc ドキュメントコメント、TypeScript の規約、コメントヘッダーが反映されます。後続の演習で PR をレビューするときに、あらためて確認します。

## Copilot cloud agent の開発環境を設定する

誰がコードを書く場合でも、通常は環境の準備とセットアップスクリプトの実行が必要です。Copilot にタスクを割り当てる場合も同じです。Copilot はソフトウェアエンジニアのように作業します。

Cloud agent は、作業環境として [GitHub Actions][github-actions] を使います。`.github/workflows/copilot-setup-steps.yml` に設定する[専用のセットアップワークフロー][setup-workflow]を作成すると、作業開始前に必要な開発ツールや依存関係を利用できるように環境をカスタマイズできます。ラボを円滑に進め、学習に集中できるよう、あらかじめ設定されています。単一の Astro アプリのために、Node.js、プロジェクトの依存関係、エンドツーエンドテスト用のブラウザーバイナリ、マイグレーションとシード済みの SQLite データベースを用意します。

```yaml
name: "Copilot Setup Steps"

# リポジトリの Actions タブからセットアップ手順をテストできます。
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # ここで必要な最小限の権限を設定します。Copilot は操作用の独自トークンを受け取ります。
    permissions:
      # セットアップでリポジトリをクローンする場合 (依存関係のインストールなど) は、`contents: read` 権限が必要です。クローンしない場合は、手順の完了後に Copilot が自動的にクローンします。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / アプリのセットアップ - Node.js (アプリ全体は Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # ビルドとテスト用にローカル SQLite データベースをマイグレーションしてシードします。
      - name: Set up the database
        run: npm run db:setup
```

一般的な GitHub ワークフローファイルと同じですが、重要な点がいくつかあります。

- `copilot-setup-steps` というジョブが1つあります。このジョブは、Copilot がプルリクエストに取り組む前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーが設定されているため、リポジトリの **Actions** タブからワークフローを手動実行できます。Copilot が実行するまで待たずに、正常に動くかテストできます。

## ドキュメントを追加する

ドキュメントの重要性は広く理解されていますが、古い情報が残っていたり、まったくなかったりするプロジェクトは少なくありません。こうした技術的負債は放置されやすく、生産性を下げ、コードベースの保守や新しいチームメンバーの受け入れを難しくします。Copilot はドキュメント作成が得意なので、cloud agent に任せるのに適した issue です。バックグラウンドで必要なドキュメントを生成します。後の演習で、作業をレビューします。

1. 新しいブラウザータブで github.com のリポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい issue ダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次の内容を入力します。

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して、割り当てダイアログを開きます。

   ![issue を Copilot に割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。
10. **Pull Requests** タブを選択します。
11. 新しく作成されたプルリクエスト (PR) を開きます。タイトルは `[WIP]: Code lacks documentation` のような名前です。PR が一覧に表示されない場合は、少し待ってからブラウザーを更新します。
12. 数分後、Copilot が TODO リストを作成します。

> [!NOTE]
> Copilot の TODO リストが PR に表示されるまで数分かかることがあります。Copilot は環境を作成し (前述のワークフローを実行)、プロジェクトを分析して、問題に取り組む最善の方法を検討しています。

13. TODO リストと、実行予定のタスクを確認します。
14. プルリクエストのタイムラインを下にスクロールし、Copilot が issue に取り組み始めたことを示す更新を確認します。
15. **View session** ボタンを選択します。

   ![Copilot セッションの表示](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 更新された状態が表示されるまで、ウィンドウの再読み込みが必要な場合があります。

16. セッションをリアルタイムでスクロールして、Copilot がどのように問題を解決しているかを確認します。コードの調査や状態の把握、計画を考えるための一時停止、コードの作成などを観察できます。

完了まで数分かかることがあります。Copilot cloud agent の主な目的は、非同期にタスクを実行し、開発者が別の作業に取り組めるようにすることです。この利点を活用するため、もう1つのタスクを cloud agent に割り当ててから、アプリケーションに機能を追加する作業を進めます。

## ゲーム詳細ページに関連ゲームのセクションを追加する

GitHub Copilot cloud agent の大きな利点は、作業を分けられることです。デザインチームのために関連ゲームのセクションを追加するタスクに時間がかからないとしても、その時間をほかの作業に使えます。Copilot cloud agent に割り当てましょう。

1. github.com のリポジトリに戻ります。
2. **Issues** タブを選択します。
3. **New issue** を選択します。
4. **Blank issue** を選択して、空のテンプレートを使います。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次の内容を入力します。

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して、割り当てダイアログを開きます。

   ![issue を Copilot に割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

まもなく、issue の最初のコメントに 👀 が表示され、Copilot が作業を始めたことが分かります。

![issue への作業開始を示す目の絵文字](../../../_images/ex4-issue-eyes-emoji.png)

Copilot は2つ目の依頼にも取り組んでいます。Copilot cloud agent はソフトウェアエンジニアと同じように作業するので、常に監視する必要はありません。完了後にレビューできます。次は、カスタムエージェントを作成して使いましょう。

## まとめと次のステップ

このレッスンでは [GitHub Copilot cloud agent][copilot-agents] を確認しました。cloud agent に issue を割り当て、非同期に作業を任せられます。技術的負債への対応、新機能の作成、別のフレームワークからのコード移行などに活用できます。

このレッスンでは、次のことを行いました。

- コード生成の環境をカスタマイズしました。
- 操作が安全に行われるようにしました。
- 範囲を明確に定めた issue の重要性を学びました。
- issue を Copilot に割り当てました。

cloud agent がバックグラウンドで作業している間に、カスタムエージェントの作成と利用に進みましょう。[Copilot cloud agent は MCP サーバー][cloud-agent-mcp]と、前のモジュールで学んだカスタム指示も利用できます。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップワークフローのベストプラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタムエージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
