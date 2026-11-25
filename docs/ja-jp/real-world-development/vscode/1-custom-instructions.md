---
title: "レッスン 1 - カスタム指示 (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Agent mode →][next-lesson]

生成 AI を使うときは、コンテキストが重要です。タスクを特定の方法で進める必要がある場合や、Copilot に知っておいてほしい背景情報がある場合は、そのコンテキストを参照できるようにします。Copilot に特定のコンテキストを伝える方法はいくつかあります。その中心となる[指示ファイル][instruction-files]を使って、コード生成に関するガイダンスを提供します。

この演習では、次のことを行います。

- リポジトリのカスタム指示とパス別の指示ファイルを使い、プロジェクト固有のコンテキスト、コーディングガイドライン、ドキュメント標準を Copilot に伝える方法を確認します。
- 既存の指示を使って、フィルタリング機能の最初のデータ部分 (publisher ヘルパー) を作成します。
- `.github/copilot-instructions.md` に新しいリポジトリ全体の標準を追加します。
- 同じプロンプトを再実行し、生成コードに新しい標準が反映されることを確認します。
- 指示の更新とフィルタリング部分を `main` にコミットし、次の演習で Copilot が最新の指示を使えるようにします。

> [!CAUTION]
> 生成コードが設定した標準から外れる場合があります。Copilot の出力は確定的ではありません。この演習では、指示の更新前後で行動がどのように変化するかを確認します。コードを一字一句同じにすることが目的ではありません。

## 指示ファイル

### シナリオ

適切な開発チームとして、Tailspin Toys には開発手法に関するガイドラインと要件があります。具体的には、次のとおりです。

- データレイヤーには、必ずユニットテストを用意します。
- UI はダークモードにし、現代的な印象にします。
- TSDoc のドキュメントコメントをコードに追加します。
- 各ファイルの先頭に、ファイルの役割を説明するコメントブロックを追加します。

指示ファイルを使うと、Copilot に適切な情報を提供し、こうした開発手法に沿ってタスクを進められます。

### カスタム指示

カスタム指示では、Copilot がコーディングスタイルや要件を理解できるように、コンテキストと希望を伝えます。コーディング規約やライブラリ、コードに含めるコメントの形式などを指定でき、より適切な提案やコードスニペットを得るのに役立ちます。リポジトリ全体に適用する指示も、特定のファイルやタスクに適用する指示も作成できます。

指示ファイルには、次の2種類があります。

- `.github/copilot-instructions.md` は、リポジトリでの**すべて**のリクエストについて Copilot に送信される単一の指示ファイルです。多くのリクエストに関係するプロジェクト全体の情報を記載します。使用する技術スタック、開発するものの概要、ベストプラクティス、全体的なガイダンスなどが含まれます。
- `.github/instructions/*.instructions.md` は、特定のタスクやファイル形式に関する指示を記載します。TypeScript や Astro などの特定の言語、UI コンポーネントの作成、ユニットテストの追加などのタスクにガイドラインを設定できます。

> [!NOTE]
> IDE で作業する場合、指示ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、リポジトリレベルの指示と、`applyTo` frontmatter を持つ `*.instructions.md` ファイルの両方をコード生成時に使います。
>
> また、Copilot は AGENTS.md や CLAUDE.md など、ほかの標準に基づく指示ファイルもサポートしています。[カスタム指示のサポート][custom-instructions-support]を参照してください。

### 指示ファイルを管理するためのベストプラクティス

指示ファイルを作るための詳しい説明は、このワークショップの範囲外です。ただし、サンプルプロジェクトの例から、一般的な使い方を学べます。

- `copilot-instructions.md` には、開発するものの説明、プロジェクト構成、全体的なコーディング標準など、プロジェクト全体に関するガイダンスを記載します。
- `*.instructions.md` ファイルには、ユニットテスト、Astro コンポーネント、データレイヤーなどのファイル形式や、特定のタスクに関する指示を記載します。
- 自然な言葉で、明確なガイダンスを記載します。コードの良い例と避けるべき例を示してください。

指示ファイルの作成方法は1つに限られません。AI の使い方と同じように、試しながらプロジェクトに合った方法を見つけましょう。

> [!TIP]
> GitHub Copilot を使うすべてのプロジェクトで、十分な指示ファイルを用意することをお勧めします。このプロジェクトには、[UI の更新][ui-instructions]や [Astro][astro-instructions]など、さまざまなタスク向けの指示ファイルがあります。
>
> Copilot に指示ファイルの生成を依頼することもできます。各環境で手順は異なります (たとえば、VS Code の **Configure Chat → Generate Agent Instructions**、Copilot CLI の `/init`)。このワークショップでは、該当する環境のレッスンで手順を説明します。
>
> テンプレートやひな形を探している場合は、指示ファイル、カスタムエージェント、その他のリソースを集めた [awesome-copilot][awesome-copilot] を確認してください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム指示ファイルを確認する

このリポジトリに用意されている指示ファイルを確認しましょう。中心となる `copilot-instructions.md` と、さまざまなタスク向けの `*.instructions.md` ファイルがあります。エディターまたは GitHub Web UI で開いてください。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの簡単な説明と、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** の中には、**GitHub Actions Workflows** に関するガイダンスもあります。これらの指示は、Copilot と行うあらゆる作業に適用されます。
3. `.github/instructions` フォルダーを開いて確認します。Astro ファイル、Drizzle データレイヤー、テストなどに関する指示があります。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドが、リポジトリルートを基準とする glob を指定しています。たとえば `**/*.test.ts` に一致する TypeScript テストファイルが対象になります。
5. このプロジェクトでユニットテストを作成する際の指示を確認します。
6. 最後に `.github/instructions/drizzle.instructions.md` を開き、末尾までスクロールします。`unit-tests.instructions.md` などの指示ファイルや、プロジェクト内の既存ファイルへのリンクがあります。大きな指示セットを小さく再利用可能なファイルに分け、Copilot に参考例を示せます (リンクのパスはリポジトリルートではなく、指示ファイルの場所を基準にしています)。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションではプロジェクトのコーディング標準を説明していますが、コード内のドキュメントはまだ必須ではありません。次の手順で、TSDoc のドキュメントコメントとファイルヘッダーコメントのルールを追加します。

## 変更用ブランチを作成する

ここでは、ベストプラクティスに従って変更用ブランチを作成します。

1. 前の演習で使った Codespace に戻ります。
2. <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押して、新しいターミナルを開きます。
3. 新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions
   ```

## 指示を更新する前に Copilot Chat を使う

> [!TIP]
> **Copilot Chat を開く**
>
> 次の演習を始める前に Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を開始します。各演習で使うモードやモデルは異なります。必要な手順をそれぞれ説明します。

カスタム指示の影響を確認するため、まず現在の指示ファイルを使った状態でプロンプトを送信します。後で指示を更新したら、同じプロンプトをもう一度送信して違いを確認します。

1. 前の演習のエディタータブをすべて閉じ、Copilot が必要なコンテキストだけを使うようにします。
2. `src/lib/publishers.ts` を開き、ヘルパーを配置する場所を Copilot に示します。
3. Chat ビューのエージェントドロップダウンで **Agent** を選択し、Copilot がファイルを変更できるようにします。

   ![Chat ビューのエージェントピッカーの画面](../../../_images/shared-chat-mode-selector.png)

4. 次のプロンプトを送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot はプロジェクトを調べて、ヘルパーファイルやテストなどを変更します。
6. 提案されたヘルパーが、最初の引数として `db` クライアントを受け取り、publisher の型付き配列を返す関数であることを確認します。これは `src/lib/*.ts` に適用される `.github/instructions/drizzle.instructions.md` のデータレイヤー規約によるものです。
7. 生成されたコードには、TSDoc のドキュメントコメントとファイルヘッダーコメントが**ない**ことを確認します。

> [!CAUTION]
> Copilot の結果は確定的ではないため、指示がなくてもドキュメントコメントが追加される場合があります。その場合も問題ありません。この演習の目的は、指示を追加した後に動作が一貫するかを確認することです。

## リポジトリ全体の新しい標準を追加する

前の説明のとおり、`.github/copilot-instructions.md` は Copilot にプロジェクト全体の情報を提供するファイルです。リポジトリのコーディング標準を記載して、コード提案の改善に役立てましょう。

1. `.github/copilot-instructions.md` をもう一度開きます。
2. 27行目付近にある **Code formatting requirements** セクションを探します。プロジェクトのコーディング標準が記載されていますが、コード内のドキュメントに関するルールはありません。そのため、生成されたヘルパーにはドキュメントコメントがありませんでした。
3. 既存の標準の直後に、次の Markdown を追加します。ファイルヘッダーコメントと TSDoc のドキュメントコメントを追加するよう Copilot に指示します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 前のレッスンで学んだように、指示ファイルはリポジトリ全体に適用する `.github/copilot-instructions.md` と、特定の言語、ファイル形式、タスクに適用する `*.instructions.md` に分けて作成できます。今回追加したドキュメントコメントのルールのように、プロジェクト全体の標準はリポジトリレベルのファイルに記載します。

## プロンプトを再実行して変化を確認する

1. Copilot Chat に戻り、**New Chat** を選択して会話をリセットします。
2. `src/lib/publishers.ts` をもう一度選択し、Copilot の対象ファイルにします。
3. 前と**同じプロンプト**を送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 今回は、提案されたファイルの先頭に次のようなコメントブロックがあることを確認します。

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. 提案された関数に次のような TSDoc コメントが含まれることを確認します。

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

新しいプロジェクト標準に従うよう Copilot を導き、次の演習で使うコードに適用しました。

## 指示とブランチをコミットしてプッシュする

指示ファイルもほかの資産と同じように、ソース管理で管理します。変更をコミットして、リポジトリにブランチをプッシュしましょう。

1. <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押して、新しいターミナルウィンドウを開きます。
2. ターミナルで次のコマンドを実行し、指示とヘルパーの変更があることを確認します。

   ```bash
   git status
   ```

3. ターミナルで次のコマンドを実行し、指示と Copilot がヘルパーの基盤に加えたすべての変更をステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # git status にテストなどの関連変更が表示された場合は、それらも追加します。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. ターミナルでブランチをリポジトリにプッシュします。

   ```bash
   git push -u origin custom-instructions
   ```

## プルリクエストを作成してマージする

ブランチをプッシュしたら、バックログにあるドキュメント標準の issue に関連付けたプルリクエストを作成します。手動で行う代わりに、すでにプロジェクトに接続されている GitHub ツールを使って Copilot に依頼しましょう。issue を探して、issue をクローズする PR を作成するようプロンプトを送ります。

> [!NOTE]
> この演習では初めて Copilot に GitHub 上の操作を依頼します。プロジェクトのテンプレートでは GitHub のツールがワークスペースに接続されています。Copilot が初めてツールを使うときに、VS Code から GitHub へのサインインを求められる場合があります。画面の案内に従って許可してください。接続方法は後の演習で Model Context Protocol として学びます。

1. Codespace で Copilot Chat を開きます。
2. <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) を押して Copilot Chat ビューを開き、エージェントピッカーで **Agent** が選択されていることを確認します。
3. 指示ファイルの更新に関する issue を探し、現在のブランチから PR を作成するよう Copilot に依頼します。指示の更新と、今後のフィルタリング作業に備えた publisher ヘルパーの基盤の両方を PR に記載します。

   ```plaintext
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot が GitHub 操作の実行を許可するよう求めたら、コマンドを確認して、適切な操作だけを **Allow** します。
5. PR が作成されたら、次のプロンプトでマージしてローカルのブランチを `main` に戻すよう依頼します。

   ```plaintext
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

6. Copilot が GitHub 操作やシェルコマンドの実行を許可するよう求めたら、コマンドを確認し、適切な操作だけを **Allow** します。

これで GitHub Copilot の助けを借りてプルリクエストを作成し、マージできました。

## まとめと次のステップ

このプロジェクトで Copilot が指示ファイルからコンテキストを読み取る方法を確認し、VS Code の Copilot Chat を使って次の作業を行いました。

- 既存の指示を使ったコード生成プロンプトを送り、Copilot が生成する内容を確認しました。
- `.github/copilot-instructions.md` に新しいリポジトリ全体の標準を追加しました。
- 同じプロンプトを再実行し、提案されたコードに新しい標準が反映されることを確認しました。
- 次の演習で使えるよう、指示の更新とヘルパーの基盤を `main` にコミットしました。

次は [agent mode][next-lesson]で指示を活用し、Copilot にコードベース全体で新機能を追加させます。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベストプラクティス][instructions-best-practices]
- [Copilot に効果的なカスタム指示を書くための5つのヒント][copilot-instructions-five-tips]
- [GitHub Copilot の個人用カスタム指示][personal-instructions]
- [Awesome Copilot — 指示ファイルやその他のリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
