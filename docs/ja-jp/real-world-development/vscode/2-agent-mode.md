---
title: "レッスン 2 - Copilot Agent Mode で機能を追加する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

アプリケーションの小さな更新でも、通常は複数のファイルを変更し、テストを実行するなどの作業が必要です。開発者は、必要なファイルを探し、変更を行い、テストを実行し、デバッグし、変更漏れのファイルを見つけ、さらに更新するという作業を繰り返します。

このような場面で役立つのが Copilot Agent Mode です。

Copilot Agent Mode は、IDE 内でより自律的に作業するよう設計されています。開発者と同じように既存のプロジェクト構成を調査し、必要な更新を行い、テストなどのタスクを実行し、見つかった問題を自動的に修正します。Agent Mode を使って、サイトに新しい機能を追加する方法を確認しましょう。

> [!NOTE]
> 名前は似ていますが、agent mode と cloud agent は異なる用途向けに作られています。Agent mode は IDE 内でタスクを実行し、すばやいフィードバックとやり取りを可能にします。Cloud agent はチームメンバーのように非同期で作業し、issue とプルリクエストを通じてやり取りします。

この演習では、次のことを学びます。

- Copilot Agent Mode がプロジェクトを調査し、関連ファイルを見つけて、複数のファイルにまたがる変更を行う方法
- GitHub Copilot Agent Mode が UI とデータレイヤーにわたって機能を実装する方法
- コードベースにマージする前に、Copilot Agent Mode が生成した変更とテストをレビューする方法

## シナリオ

ゲームの一覧が増えてきたため、ユーザーがカテゴリやパブリッシャーで絞り込めるようにします。前の演習では publisher ヘルパーを追加しました。次は、残りのデータレイヤー、UI、テストを Copilot Agent Mode で実装します。

## Tailspin Toys の Web サイトを実行する

変更を加える前に、Tailspin Toys の Web サイトを確認し、現在の機能を理解しましょう。

このサイトは開発者向けテーマのボードゲーム・クラウドファンディングプラットフォームです。ゲームの一覧と詳細を表示できます。単一の Astro アプリで、ビルド時にページを静的 HTML として生成します。ページは frontmatter 内で Drizzle ORM を使ってローカルの SQLite データベースに直接問い合わせます。独立したバックエンド API やクライアント側 UI フレームワークはありません。再利用可能なデータアクセスヘルパーは `src/lib/` に置き、インタラクティブな動作には標準 DOM API を使う、小規模な Astro `<script>` を使用します。

### Web サイトを起動する

Web サイトを簡単に実行できるよう、単一の Astro 開発サーバーを起動する `npm run dev` タスクが用意されています。GitHub Codespace で次の手順を実行します。

1. Codespace に戻ります。前の演習後なので、`main` にいるはずです。
2. <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押して、Codespace 内に新しいターミナルを開きます。
3. フィルタリング作業用のブランチを作成して切り替えます。

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 次のコマンドを実行して Web サイトを起動します。

   ```bash
   npm run dev
   ```

   Astro 開発サーバーが起動すると、次のような URL を含むメッセージが表示されます。

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> `http://localhost:4321` を開くためのダイアログが表示された場合は、**x** を選択して閉じます。

5. ターミナルの Astro サーバーアドレス `http://localhost:4321` を、<kbd>Command</kbd> (Mac) または <kbd>Ctrl</kbd> (Windows/Linux) を押しながら選択して、Web サイトを開きます。

> [!NOTE]
> Codespace のターミナルで localhost URL を選択すると、自動的に `https://<your-codespace-name>-4321.app.github.dev/` に転送されます。これは Codespace の Web サーバーをホストするためのプライベートトンネルです。

### Web サイトを確認する

Web サイトを起動したら、機能を確認します。主なページは次のとおりです。

- **ホームページ**: ボードゲームの一覧と、タイトル、画像、説明を表示します。
- **ゲーム詳細ページ**: ゲームを選択すると、タイトル、説明、パブリッシャー、カテゴリなどの情報を確認できます。

## Copilot でバックログを確認する

> [!TIP]
> **Copilot Chat を開く**
>
> 次の演習を始める前に Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を開始します。各演習で使うモードやモデルは異なります。必要な手順をそれぞれ説明します。

Web サイトの最初の実装は動作していますが、さらに機能を追加したいと考えています。まずバックログを確認しましょう。テンプレートからプロジェクトを作成すると、issue のバックログも自動的に作成されています。GitHub Copilot に内容を表示するよう依頼します。

1. Chat ビューのエージェントドロップダウンで **Agent** を選択します。**Agent** はファイルにまたがる変更を計画・実装し、ターミナルコマンドを実行し、ツールを呼び出します。

   ![Chat ビューのエージェントピッカーの画面](../../../_images/shared-chat-mode-selector.png)

2. 利用可能なモデル一覧から **Claude Sonnet 4.5** を選択します。

> [!CAUTION]
> ワークショップの作成者が特定のモデルを推奨するものではありません。このワークショップの作成時に Claude Sonnet 4.5 を使用したため、手順にも記載しています。提案コードの一貫性を高め、演習を進めやすくすることを意図しています。ただし、LLM の出力は確定的ではありません。手順と異なる提案が表示されることもあります。これは想定どおりです。

> [!NOTE]
> LLM の出力は確定的ではないため、Copilot が別の MCP コマンドを使う場合がありますが、タスクは完了できるはずです。

3. 次のプロンプトを Copilot に送り、issue のバックログを確認します。

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. **Continue** を選択して、すべての issue を一覧表示するコマンドを実行します。
5. 生成された issue の一覧を確認します。

Copilot はユーザーに最も役立つと思われる項目を基準に、優先順位も付けています。

## 指示ファイルを確認する

エージェントにコードを生成させる前に、作業のコンテキストを Copilot に伝える指示ファイルを確認しましょう。Web サイトへの機能追加方法に関するコンテキストが記載された、[ユーザーインターフェイス (UI)](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md) ファイルを使います。

1. Codespace で `.github/instructions/ui.instructions.md` に移動します。
2. 機能追加の進め方に関するガイダンスを確認します。次の内容が含まれます。
   - アーキテクチャの概要
   - コンポーネントの設計、テスト可能性、アクセシビリティの原則
   - Astro、Tailwind CSS、Drizzle などのファイル形式に対応する指示ファイルへのリンク

> [!TIP]
> 指示ファイルから別の指示ファイルやプロジェクト内のファイルを参照できます。パスは指示ファイルの場所を基準にするため、再利用や、大きな指示を小さく管理しやすい単位に分けること、参考例やテンプレートを示すことができます。

## フィルタリング機能を実装する

フィルタリングを完成させるには、少なくとも次の3種類の更新が必要です。

- データレイヤー (`src/lib/`) に残りのフィルタリングロジックを追加または調整します。
- フィルタリング動作のテストを追加または更新します。
- ゲーム一覧ページにフィルタリング UI を追加します。

さらに、コードベースにマージする前にテストを実行し、合格させる必要があります。Copilot Agent Mode にこれらのタスクを任せます。

1. 現在の Copilot 会話を続けるか、**New Chat** を選択して新しい会話を開始します。
2. **Add Context**、**Instructions**、**ui** の順に選択して、指示ファイルを指定します。

   ![UI 指示ファイルを選択する画面](../../../_images/ex3-select-instructions-file.png)

3. Chat ビューのエージェントドロップダウンで **Agent** が選択されていることを確認します。

   ![Chat ビューのエージェントピッカーの画面](../../../_images/shared-chat-mode-selector.png)

4. モデルが **Claude Sonnet 4.5** であることを確認します。
5. バックログ内の関連 issue に基づいて機能を実装するよう、次のプロンプトで Copilot に依頼します。

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Copilot がプロジェクトを調査し、機能に関連するファイルを探す様子を確認します。データレイヤーのヘルパー、UI、テストなどが見つかります。次にファイルを変更し、テストを実行します。

   ![Copilot がプロジェクト内のファイルを調査する画面](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot はプロジェクトの調査、ファイルの変更、テストの実行などを行うため、時間がかかることがあります。作業中、コードエディターに **Keep** と **Undo** のボタンが表示される場合があります。作業が完了するとすべての変更に **Keep** または **Undo** が表示されるため、作業中に選択する必要はありません。

7. Copilot に求められたら、**Continue** を選択してテストを実行します。

   ![Copilot Chat ペインに表示されたテスト実行の確認ダイアログ](../../../_images/ex3-agent-mode-run-tests.png)

8. 作業の途中で停止したり、テストが失敗したりする場合があります。問題ありません。Copilot はコード生成とテストを繰り返し、エラーが見つからなくなるまで作業を続けます。

   ![Copilot Agent Mode の完了済みチャットセッション](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 生成されたコードに問題がないか確認します。

> [!CAUTION]
> Copilot やほかの AI ツールが生成したコードは、必ずレビューしてください。

10. Web サイトを表示しているブラウザーに戻り、新しい機能を試します。
11. すべて動作し、コードのレビューも終わったら、Copilot Chat ウィンドウで **Keep** を選択します。

## まとめと次のステップ

おめでとうございます。この演習では、GitHub Copilot Agent Mode を使って Tailspin Toys の Web サイトに機能を追加しました。次のことを学びました。

- GitHub Copilot Agent Mode が UI とデータレイヤーにわたって機能を実装する方法
- Copilot Agent Mode がプロジェクトを調査し、関連ファイルを見つけて、複数のファイルにまたがる変更を行う方法
- コードベースにマージする前に、Copilot Agent Mode が生成した変更とテストをレビューする方法

次は [Playwright MCP サーバーで機能をテストし][next-lesson]、プルリクエストを作成します。

### 追加の演習 — ページ分割を実装する

ゲームの一覧が増えると、ページ分割が必要になります。この演習で学んだことを使い、Copilot にページ分割を実装するよう依頼してみましょう。次の点を検討してください。

- 指示ファイルを使うなど、既存のベストプラクティスに従います。
- ページサイズをユーザーが選べるようにするか、固定値にするかなど、ページ分割の方法を検討します。
- 希望どおりの実装にするため、Copilot に必要なガイダンスをプロンプトに含めます。
- Copilot に追加の変更を依頼し、コンテキストを提供しながら作業を繰り返す必要がある場合があります。Copilot との作業では通常の進め方です。

## リソース

- [Copilot の ask、edit、agent mode: それぞれの役割と使い分け][choose-mode]
- [VS Code の agent mode][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
