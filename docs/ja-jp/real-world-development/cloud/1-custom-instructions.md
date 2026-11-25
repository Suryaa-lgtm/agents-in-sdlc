---
title: "レッスン 1 - カスタム指示 (Cloud agent)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を使うときは、コンテキストが重要です。タスクを特定の方法で進める必要がある場合や、Copilot に知っておいてほしい背景情報がある場合は、そのコンテキストを参照できるようにします。[指示ファイル][instruction-files]を使うと、何を実行するかだけでなく、その方法も Copilot に伝えられます。

この演習では、次のことを行います。

- リポジトリのカスタム指示とパス別の指示ファイルを使い、プロジェクト固有のコンテキスト、コーディングガイドライン、ドキュメント標準を Copilot に伝える方法を確認します。
- `.github/copilot-instructions.md` に新しいリポジトリ全体の標準を追加します。

> [!NOTE]
> VS Code や CLI の環境とは異なり、この演習ではプロンプトの実行前と実行後を比較しません。Copilot cloud agent は GitHub issue を使って非同期に作業するため、リアルタイムの比較が難しいからです。後続の演習で cloud agent が作成したプルリクエストをレビューするときに、指示ファイルの影響を確認できます。

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

- `.github/copilot-instructions.md` は、リポジトリでの**すべて**のリクエストについて Copilot に送信される単一の指示ファイルです。Copilot に送る多くのチャットや CLI のリクエストに関係する、プロジェクト全体の情報を記載します。使用する技術スタック、開発するものの概要、ベストプラクティス、全体的なガイダンスなどが含まれます。
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

このリポジトリに含まれる指示ファイルを確認しましょう。中心となる `copilot-instructions.md` と、さまざまなタスク向けの `*.instructions.md` ファイルがあります。エディターまたは GitHub の Web UI で開いてください。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの簡単な説明と、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** の中には、**GitHub Actions Workflows** に関するガイダンスもあります。これらの指示は、Copilot と行うあらゆる作業に適用されます。
3. `.github/instructions` フォルダーを開いて確認します。Astro ファイル、Drizzle データレイヤー、テストなどに関する指示があります。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドが、リポジトリルートを基準とする glob を指定しています。たとえば `**/*.test.ts` に一致する TypeScript テストファイルが対象になります。
5. このプロジェクトでユニットテストを作成する際の指示を確認します。
6. 最後に `.github/instructions/drizzle.instructions.md` を開き、末尾までスクロールします。`unit-tests.instructions.md` などの指示ファイルや、プロジェクト内の既存ファイルへのリンクがあります。大きな指示セットを小さく再利用可能なファイルに分け、Copilot に参考例を示せます (リンクのパスはリポジトリルートではなく、指示ファイルの場所を基準にしています)。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションではプロジェクトのコーディング標準を説明していますが、コード内のドキュメントはまだ必須ではありません。次の手順で、TSDoc のドキュメントコメントとファイルヘッダーコメントのルールを追加します。

## リポジトリ全体の新しい標準を追加する

この演習で編集するのは、プロジェクト全体のルールを追加する1か所です。コード内に TSDoc のドキュメントコメントとファイルヘッダーコメントを記載するよう指定します。後続の演習で issue を割り当てると、cloud agent はこの標準を参照します。

編集の前に、変更用ブランチを作成します。cloud agent は issue の対象ブランチから指示を読み込みますが、変更をきれいにコミットしておきます。

1. Codespace のターミナルで、新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

前のセクションで説明したように、`.github/copilot-instructions.md` は Copilot にプロジェクト全体の情報を提供するファイルです。リポジトリのコーディング標準を記載して、コード提案の改善に役立てましょう。

1. `.github/copilot-instructions.md` をもう一度開きます。
2. 27行目付近にある **Code formatting requirements** セクションを探します。プロジェクトのコーディング標準が記載されていますが、コード内のドキュメントに関するルールはありません。そのため、生成されたヘルパーにはドキュメントコメントがありませんでした。
3. 既存の標準の直後に、次の Markdown を追加します。すべてのファイルにヘッダーコメントを付け、TSDoc のドキュメントコメントを追加するよう Copilot に指示します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 前のレッスンで学んだように、指示ファイルはリポジトリレベルの `.github/copilot-instructions.md` に置いて全体に適用することも、特定の言語、ファイル形式、タスク向けの `*.instructions.md` に記載することもできます。追加したドキュメントコメントのルールのように、プロジェクト全体の標準はリポジトリレベルのファイルに記載します。

## 指示の変更をコミット、プッシュ、マージする

cloud agent は、issue が対象とするブランチから指示ファイルを読み込みます。次の演習で Copilot に割り当てる issue は `main` からブランチを作成するため、cloud agent が指示を参照できるよう、変更を `main` にマージする必要があります。

1. 変更をステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` へのプルリクエストを開き、マージします。次の演習で issue を割り当てると、cloud agent は更新された指示を読み込みます。

> [!TIP]
> このワークショップでは `main` に直接作業してもかまいません。その場合はブランチの作成を省略して、`main` に直接コミットします。ブランチを使う手順は、実際のプロジェクトに近い作業方法を体験するためのものです。

## まとめと次のステップ

このプロジェクトで Copilot が指示ファイルからコンテキストを読み取る方法を確認し、`.github/copilot-instructions.md` にリポジトリ全体の標準を追加しました。残りの演習で cloud agent が作成するプルリクエストに、その標準が適用されているか確認します。

次は、初めての issue を[Copilot cloud agent に割り当てます][next-lesson]。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベストプラクティス][instructions-best-practices]
- [Copilot に効果的なカスタム指示を書くための5つのヒント][copilot-instructions-five-tips]
- [Awesome Copilot — 指示ファイルやその他のリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
