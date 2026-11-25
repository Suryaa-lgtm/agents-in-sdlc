---
title: "レッスン 6 - Playwright MCP で機能を検証する"
description: "Copilot CLI で Playwright MCP の設定を確認または追加し、ブラウザーからフィルタリング機能を試します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

これまでに説明したとおり、コードを書くことだけが開発ではありません。データや外部サービスを扱い、Copilot が利用できる自動化機能を追加することも必要です。MCP サーバーを使うと、Copilot CLI に組み込まれている機能を超えて、さらに多くのツールやサービスを利用できます。

このレッスンでは、次のことを行います。

- Model Context Protocol (MCP) とは何か、Copilot CLI でどう利用されるかを理解します。
- まだ利用できない場合は、Playwright MCP サーバーを追加します。
- エージェントにブラウザーを操作させ、フィルタリング機能を確認します。

## Model Context Protocol (MCP) とは

[Model Context Protocol (MCP)][mcp-blog-post] は、AI エージェントが外部のツールやサービスと通信するための仕組みです。MCP を使うと、AI エージェントは外部のツールやサービスとリアルタイムに通信できます。最新情報にアクセスしたり、ユーザーに代わって操作を実行したりできます。

これらのツールやリソースには MCP サーバーを通じてアクセスします。MCP サーバーは AI エージェントと外部のツールやサービスの間をつなぎます。それぞれの MCP サーバーは、エージェントが利用できるツールやリソースのセットを提供します。

よく使われる MCP サーバーの例を紹介します。

- **[GitHub MCP Server][github-mcp]**: GitHub リポジトリ、issue、プルリクエストを管理する API にアクセスします。
- **[Playwright MCP Server][playwright-mcp-server]**: Playwright を使ったブラウザー自動化機能を提供します。

ほかにも多くの MCP サーバーが利用できます。GitHub は、エコシステム内での発見や貢献を促進するために[MCP レジストリ][mcp-registry]をホストしています。

> [!CAUTION]
> MCP サーバーは、プロジェクトのほかの依存関係と同じように扱ってください。使用前にソースコードを確認し、公開元を検証し、セキュリティへの影響を検討してください。

## Playwright MCP サーバーを追加する

まだ Playwright MCP サーバーが利用できない場合は、Copilot がユーザーと同じようにサイトを操作できるように追加します。

> [!NOTE]
> Copilot CLI で Playwright MCP がすでに設定されている場合は、この手順を省略して次のセクションに進んでください。

1. Codespace に戻ります。
2. Copilot CLI で次のコマンドを入力し、MCP サーバー追加ダイアログを開きます。

   ```plaintext
   /mcp add
   ```

3. 名前として `playwright` を入力し、<kbd>Tab</kbd> を押します。
4. <kbd>Enter</kbd> を押してサーバーの種類を **STDIO** に設定し、<kbd>Tab</kbd> を押します。
5. **Command** ダイアログに次の内容を貼り付けます。

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. <kbd>Control</kbd>+<kbd>S</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) を押して、新しい MCP サーバーを保存します。
7. <kbd>Esc</kbd> を押して MCP ダイアログを終了します。

## Copilot に Playwright で機能を確認させる

これまでは機能が期待どおりに動くことを手動で確認しました。今度は Copilot で利用できる Playwright MCP サーバーを使って、同じ確認を行いましょう。

1. 次のプロンプトを使って、Playwright MCP サーバーで機能を検証するよう Copilot に伝えます。

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> 通常は MCP サーバーを指定しなくても、Copilot が適切なサーバーを判断します。ただし、使用するサーバーが分かっている場合は、指示しておくと結果の一貫性が高まり、トークンも節約できます。

2. Copilot がブラウザー上で機能を確認するために実行する手順を見ます。
3. 報告を読み、すべて期待どおりに動作していることを確認します。

Copilot はサーバーを起動し、Playwright でサイトを操作し、作業後にサーバーを停止して結果を報告します。

## まとめと次のステップ

おめでとうございます。Copilot CLI から Playwright MCP サーバーを使い、実際のブラウザーで機能を確認しました。次のことを行いました。

- Model Context Protocol (MCP) とは何か、Copilot CLI でどう利用されるかを学びました。
- まだ利用できない場合は、Playwright MCP サーバーを追加しました。
- エージェントにブラウザーを操作させ、フィルタリング機能を確認しました。

次は、スキルとブラウザーツールを組み合わせる[QA カスタムエージェントを作成します][next-lesson]。

## リソース

- [MCP とは何か、なぜ話題になっているのか][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [Copilot CLI に MCP サーバーを追加する][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
