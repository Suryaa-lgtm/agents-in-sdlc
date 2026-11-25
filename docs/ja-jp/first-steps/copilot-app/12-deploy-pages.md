---
title: "レッスン 12 - GitHub Pages でサイトをデプロイする"
description: "GitHub Copilot app を使って Pages ワークフローを設定し、プルリクエストをレビューして、公開された Space Quiz を確認します。"
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

Space Quiz を GitHub Pages にデプロイして、誰でもアクセスできる場所に公開しましょう。Copilot はワークフローの準備やデプロイ手順の案内を行えますが、変更をレビューし、サイトが公開されたことを確認するのはあなたの役目です。

このレッスンでは、次のことを行います。

- Copilot に GitHub Pages デプロイの設定を依頼します。
- マージする前にワークフローとプルリクエストをレビューします。
- デプロイを進め、公開されたサイトを確認します。

## シナリオ

Space Quiz はすでに GitHub リポジトリにありますが、まだ簡単に試せる方法がありません。単一ファイルのサイトを GitHub Pages で公開すれば、サーバーやランタイム依存関係を追加せずに公開 URL からアクセスできるようになります。

## Copilot にデプロイの準備を依頼する

> [!WARNING]
> プルリクエストを作成すると、コードがコミットおよびプッシュされることがあります。このプロンプトを送る前に、承認設定と送信先リポジトリを確認してください。**すべて承認**に設定されている場合、個別の確認は表示されません。

`space-quiz` の Copilot app セッションで、次のプロンプトを送信します。

```plaintext
Prepare a GitHub Pages deployment for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages after changes reach the default branch. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and report its link and any required Pages settings or permissions. Do not merge, enable auto-merge, change Pages settings, or deploy. Stop and wait for my review.
```

## ワークフローとプルリクエストをレビューする

1. README は、リポジトリにまだ存在しない場合に限って追加されていることを確認します。
2. プルリクエストの変更を確認します。ワークフローのビルド手順とデプロイ手順、トリガー、権限も確認してください。
3. ワークフローが、マージされていないプルリクエストではなくデフォルトブランチからデプロイすることを確認します。
4. 必要な修正を依頼し、更新後の差分をレビューします。マージを許可する前に、必須のプルリクエストチェックが通るまで待ちます。

## マージとデプロイを許可する

> [!WARNING]
> 次のプロンプトを送ると、レビュー済みのプルリクエストのマージ、リポジトリの Pages 設定変更、サイトの公開をエージェントに許可します。レビューを完了し、リポジトリとプルリクエストを確認してから送信してください。承認設定によっては、追加の確認なしにこれらの操作が実行されます。

`<PR_NUMBER>` をレビューしたプルリクエストの番号に置き換えてから、別のプロンプトとして送信します。

```plaintext
I have reviewed pull request <PR_NUMBER> in this repository and authorize its merge and deployment. Enable GitHub Pages using GitHub Actions, merge that pull request only after required checks pass, and monitor the deployment until it succeeds. Report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
```

![3段階の図。Space Quiz のプルリクエストがマージされ、GitHub Actions の Deploy website 実行で Build website、Upload artifact、Deploy to Pages の各ステップが成功し、yourname.github.io/space-quiz/ で公開された Space Quiz が表示されている。](../../../_images/first-steps-app-pages-deploy.svg)

## デプロイを確認する

1. GitHub Actions のデプロイ実行が成功するまで確認します。
2. 報告された URL を開き、Space Quiz が読み込まれることを確認します。

エージェントが Pages の有効化やプルリクエストのマージを行えない場合は、案内された手順に従ってください。デプロイが成功し、公開サイトが読み込まれるまでは完了とみなさないでください。

## まとめと次のステップ

Space Quiz が公開され、エージェントの報告だけに頼らずデプロイを確認できました。続けて[レッスン 13: レビューと次のステップ][next-lesson]に進みましょう。

[next-lesson]: ../13-review/
