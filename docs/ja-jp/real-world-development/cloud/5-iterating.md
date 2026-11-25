---
title: "レッスン 5: GitHub Copilot の作業を繰り返し改善する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

## 作業をレビューする

このラボでは、GitHub Copilot を使ってユーザー体験を改善し、機能を追加する複数のタスクに取り組みました。コードにドキュメントを追加し、デザインチームが試せる関連ゲーム機能を作り、ハイコントラストとライトモードの切り替えを含むアクセシビリティ機能を実装するよう依頼しました。コードの変更を確認し、必要に応じて Copilot にフィードバックを送って作業を改善しましょう。

### シナリオ

これまでに何度も説明したように、生成 AI を導入しても、ソフトウェア設計と DevOps の基本は変わりません。生成されたコードをレビューし、通常の DevOps プロセスに沿って作業する必要があります。チーム全員によるレビューを有効にする前に、ドキュメント、関連ゲーム機能、アクセシビリティ機能について GitHub Copilot が提案した変更を確認しましょう。

## セキュリティと GitHub Copilot cloud agent

Copilot cloud agent は監視なしで非同期にタスクを実行するため、安全性を保つための制約があります。

- Copilot はリポジトリへの読み取りアクセス権を持ち、コード作成に使うブランチ**だけ**に書き込みアクセス権を持ちます。
- Cloud agent は GitHub Actions 内で実行され、作業用の独立した一時環境を作成します。
- GitHub Actions のワークフローを実行する前に、人間による承認が必要です。
- MCP サーバーを含む[外部リソースへのアクセスは、デフォルトで制限されています](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)。

## 生成されたドキュメントをレビューする

GitHub Copilot cloud agent が最初に作成したプルリクエスト (PR)、つまりコードへのドキュメント追加を確認しましょう。GitHub.com の標準的な PR インターフェイスを使います。

> [!NOTE]
> PR を開くと、GitHub Copilot がファイアウォールでブロックされているという警告が表示される場合があります。Copilot は外部 MCP サーバーへの呼び出しなど、外部リソースへのアクセスがデフォルトで制限されているため、これは**想定どおり**です。必要であれば、[Copilot cloud agent のファイアウォールをカスタマイズまたは無効化][agent-firewall]できます。

1. github.com のリポジトリに戻ります。
2. **Pull Requests** を選択して PR の一覧を開きます。
3. **Add missing documentation** などのタイトルのプルリクエストを開きます。

> [!NOTE]
> Copilot がまだ作業中の場合、プルリクエストに **[WIP]** が付いています。その場合は作業が完了するまで待ちます。数分かかることがあります。休憩を取ったり、学んだことを振り返ったりしてください。

4. PR の準備ができたら **Files changed** タブを選択し、変更を確認します。

   ![Files changed タブ](../../../_images/shared-pr-files-changed.png)

5. 新しく追加された TSDoc のドキュメントコメントや、更新されたコードを確認します。具体的な変更内容は状況によって異なります。

   変更を確認するときは、TSDoc のドキュメントコメント、TypeScript の規約、ファイルヘッダーコメントを探します。これらは、レッスン 2 の最初に確認したカスタム指示ファイルによるものです。

6. 更新内容をレビューして問題がなければ、**Conversation** タブに戻り、下にスクロールします。
7. ワークフローの承認待ちを示す表示を探します。
8. 承認待ちのワークフローがある場合は、**Approve and run workflows** を選択します。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. プルリクエストのチェック欄でワークフローがキューに追加されたことを確認します。単一の Astro アプリのプロジェクトチェックが成功するまで、数分かかる場合があります。

## GitHub Copilot に変更を依頼する

Copilot との PR 作業は一方通行ではありません。チームメンバーと同じように、プルリクエストやコードへのインラインコメントで Copilot にメンションできます。Copilot はコメントを確認し、対応するための新しいセッションを開始します。結果は確定的ではないため、決まった依頼文はありません。たとえば、次のような更新を依頼できます。

- 各コードファイルの先頭に、ファイルの内容を簡単に説明するコメントヘッダーを追加する。
- TypeScript と Astro のファイルに TSDoc のドキュメントコメントを追加する。
- Astro アプリの構造を説明する README を作成する。

1. 上記の案や、コードベースに追加したいドキュメントについて、**@copilot** をメンションして変更を依頼するコメントを追加します。
2. **View Session** を選択し、Copilot が作業する様子を確認します。Copilot は更新のために新しいセッションを開始します。
3. **Back to pull request** を選択すると、プルリクエストに戻れます。

   ![Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Copilot が変更を完了すると、PR に新しいコミットが表示されます。
5. **Files changed** タブを選択して変更をレビューします。

問題がなければ、レビュー準備ができた状態にドラフト PR を変更し、`main` ブランチにマージできます。

![PR をレビュー準備完了に変更する](../../../_images/ex7-ready-for-review.png)

## 関連ゲーム機能をレビューする

ゲーム詳細ページへの関連ゲーム表示を依頼した issue に対し、Copilot が作成した PR を確認しましょう。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Show related games on the game details page** などのタイトルの PR を選択します。
4. **Files changed** タブを選択して、生成されたコードをレビューします。
5. 更新を確認して問題がなければ、**Conversation** タブに戻り、下にスクロールします。
6. ワークフローの承認待ちを示す表示を確認します。
7. 承認待ちのワークフローがある場合は、**Approve and run workflows** を選択します。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

8. プルリクエストのチェック欄でワークフローがキューに追加されたことを確認します。単一の Astro アプリのプロジェクトチェックが成功するまで、数分かかる場合があります。
9. **省略可能:** Codespace でこのブランチに切り替えて、関連ゲーム機能を手動でテストできます。Codespace に移動してターミナルを開き、次のコマンドを実行します (`<branch-name>` は Copilot が作成したブランチ名、たとえば **copilot/fix-8** に置き換えます)。

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Copilot が関連ゲーム機能を作成しました。前の作業と同じように、Copilot cloud agent に変更を依頼して、繰り返し改善できます。たとえば、表示する関連ゲームの数を調整したり、コメントヘッダーと TSDoc のドキュメントコメントを追加したりできます (この issue はカスタム指示を更新する**前**に割り当てたことを思い出してください)。**Conversation** タブにコメントを追加すると、Copilot が内容を確認して新しいセッションを開始します。

## アクセシビリティ機能をレビューする

最後に、アクセシビリティ用カスタムエージェントが実装した機能を確認します。この PR にはレッスン 3 で依頼したハイコントラストモードと、レッスン 4 で mission control から追加を依頼したライトモードの両方が含まれているはずです。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Add high contrast mode to website** などのタイトルの PR を選択します。

> [!NOTE]
> Copilot がまだ作業中の場合、プルリクエストに **[WIP]** が付いています。その場合は作業が完了するまで待ちます。数分かかることがあります。

4. **Files changed** タブを選択して、生成されたコードをレビューします。
5. 実装を確認し、特に次の点を確認します。
   - モードを切り替える UI コンポーネント
   - ユーザー設定を保持するためのローカルストレージの利用
   - ハイコントラストモードとライトモードの CSS またはスタイル変更
   - アクセシビリティ属性 (ARIA ラベル、キーボード操作など)
   - モード切り替えを管理する JavaScript/TypeScript コード

6. 更新をレビューして問題がなければ、**Conversation** タブに戻り、下にスクロールします。
7. ワークフローの承認待ちを示す表示を確認します。
8. 承認待ちのワークフローがある場合は、**Approve and run workflows** を選択します。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. プルリクエストのチェック欄でワークフローがキューに追加されたことを確認します。単一の Astro アプリのプロジェクトチェックが成功するまで、数分かかる場合があります。
10. **省略可能:** Codespace でこのブランチに切り替え、アクセシビリティ機能を手動でテストできます。Codespace に移動してターミナルを開き、次のコマンドを実行します (`<branch-name>` は Copilot が作成したブランチ名に置き換えます)。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    その後、アプリケーションを起動し、ブラウザーでハイコントラストとライトモードの切り替えをテストします。ページを再読み込みしても設定が保持されることを確認してください。

アクセシビリティ用カスタムエージェントが、アクセシビリティのベストプラクティスに沿って機能を実装するよう Copilot を導いたことが分かります。アクセシビリティ上の懸念や改善点があれば、前の PR と同様にコメントで **@copilot** に更新を依頼できます。

## 省略可能な演習 — さらに作業を委任する

cloud agent は、現実のバックログのタスクを任せて、別の作業に移れる場面で役立ちます。習慣として身につけるため、リポジトリに issue を追加して Copilot に割り当ててみましょう。

- ゲーム詳細ページに支援者向けの関心フォームを作成する。
- ゲーム一覧ページにページネーションを実装する。
- データアクセスヘルパーに入力検証とエラー処理を追加する。

## まとめ

Cloud agent の環境で一連の演習を完了しました。次のことを行いました。

- このリポジトリに用意されたカスタム指示ファイルを確認し、cloud agent の出力への影響を確認しました。
- issue を Copilot cloud agent に割り当て、環境のセットアップ、計画、非同期の実行を観察しました。
- アクセシビリティ用カスタムエージェントを作成して使い、ハイコントラストとライトモードの切り替えを追加しました。
- Copilot agents ページを mission control として使い、作業中にアクセシビリティセッションを監視して案内しました。
- cloud agent が作成したプルリクエストをレビューし、`@copilot` に変更を依頼してワークフローを承認しました。

## レビューと次のステップ

Cloud agent の演習を完了しました。ほかの環境の演習では、ここで学んだ内容を別の方法で実践できます。

- 🖥️ **[VS Code 環境][vscode]** — IDE から Copilot Chat の agent mode と MCP 統合を試します。
- 💻 **[CLI 環境][cli]** — Plan と Autopilot の各モード、エージェントスキル、QA カスタムエージェント、Playwright MCP、Agent Merge、省略可能な `/delegate` による cloud agent への連携を使い、ターミナルから2つの変更をレビューしてリリースします。

自分のリポジトリでは、次の内容も試してください。

- リファクタリングやテストカバレッジの issue を cloud agent に割り当てる。
- 別の分野向けのカスタムエージェントを作成する。
- 別の技術スタック向けに `copilot-setup-steps.yml` を設定する。

## リソース

- [GitHub Copilot][github-copilot]
- [Copilot agents について][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップワークフローのベストプラクティス][cloud-agent-best-practices]
- [Copilot cloud agent のファイアウォールを設定する][agent-firewall]

---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
[previous-lesson]: ../4-managing-agents/
[vscode]: ../../vscode/
[cli]: ../../cli/
