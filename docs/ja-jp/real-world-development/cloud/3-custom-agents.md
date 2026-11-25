---
title: "レッスン 3 - カスタムエージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタムエージェントとは

GitHub Copilot の[カスタムエージェント][custom-agents-concept]を使うと、開発ワークフロー内の特定のタスクや分野に合わせて、特化した AI アシスタントを作成できます。リポジトリの `.github/agents` フォルダーに Markdown ファイルを置いてエージェントを定義し、対象の作業を効果的に進めるための集中的な指示、ベストプラクティス、コーディングパターン、分野固有の知識を Copilot に与えます。チームの専門知識を再利用可能なエージェントにまとめることもできます。たとえば、[WCAG][wcag] 準拠を確認するアクセシビリティエージェント、安全なコーディング手法に従うセキュリティエージェント、一貫したテストパターンを守るテストエージェントなどです。

カスタムエージェントは、プロジェクト内の `.github/agents` フォルダーか、グローバルな `~/.copilot/agents` にある Markdown ファイルで定義します。各ファイルには、少なくとも `name` と `description` を含む YAML frontmatter と、エージェントの動作、専門知識、指示を定める Markdown プロンプトを記述します。

### カスタムエージェントとエージェントスキルの違い

カスタムエージェントと[エージェントスキル][agent-skills-concept]には、役割が重なる部分があります。どちらも主に Markdown ファイルで定義し、AI に作業方法を伝えます。簡潔に言うと、**カスタムエージェントは作業者、スキルはツール**です。

カスタムエージェントは独自のコンテキストウィンドウを持ち、作業の一部としてスキルやほかのエージェントを調整するように設計されています。この演習では、アクセシビリティのカスタムエージェントがサイトをアクセシビリティガイドラインに照らして確認・更新します。その作業の一環として、プルリクエストのワークフローを進めるスキルやテストを実行・管理するスキルを呼び出すこともできます。

> [!NOTE]
> カスタムエージェントの作成方法に、唯一の正解はありません。AI のほかの使い方と同様に、環境やシナリオに合わせてテストし、改善してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

このレッスンでは、カスタムエージェントを使って次のことを学びます。

- カスタムエージェントの定義方法
- タスクをカスタムエージェントに割り当てる方法

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず、すべてのユーザーがクラウドファンディングプラットフォームを利用できるようにしたいと考えています。最近のユーザーフィードバックでは、テキストと背景色のコントラストが十分でないため、現在のダークテーマが読みにくいと感じるユーザーがいることが分かりました。このアクセシビリティの課題に対応するため、デザインチームはユーザーが切り替えられるハイコントラストモードを求めています。

アクセシビリティは重要なため、できるだけ早く実装したいと考えています。カスタムエージェントを使って機能を生成しましょう。

## アクセシビリティ用カスタムエージェントを確認する

アクセシビリティ用カスタムエージェントは、あらかじめ用意されています。Copilot を導く方法を理解するため、内容を確認しましょう。

Codespace に戻り、アクセシビリティ用カスタムエージェントのファイルを確認します。

1. `.github/agents/accessibility.md` を開きます。
2. `name` と `description` フィールドがある YAML frontmatter を確認します。

> [!CAUTION]
> カスタムエージェントには、`name` と `description` を含む frontmatter が必要です。

3. 続くセクションを読み、次の内容を確認します。
   - アクセシブルな Web サイトのコード生成に関する主な責任
   - アクセシビリティのベストプラクティス
   - HTML、CSS、JavaScript のコード例
   - よくある問題や間違い

## issue を作成して割り当てる

Mission control は、環境内のすべてのエージェントを操作する場所です。Copilot cloud agent にタスクを割り当て、監視し、作業中のセッションに追加の指示を出せます。まず Copilot にハイコントラストモードを追加するタスクを割り当てます。

1. リポジトリに移動します。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい issue ダイアログを開きます。
4. **Blank issue** を選択して issue を作成します。
5. **Title** に `Add high contrast mode to website` と入力します。
6. **Description** に次の内容を入力します。

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して、割り当てダイアログを開きます。
9. 一覧から **Accessibility agent** を選択します。

   ![cloud agent の割り当て画面。カスタムエージェントと Accessibility が強調表示されている](../../../_images/ex5-select-custom-agent.png)

10. **Assign** を選択します。
11. Copilot がバックグラウンドで作業を始めます。

## まとめと次のステップ

このレッスンでは、特定のタスクや分野に合わせて調整する [GitHub Copilot のカスタムエージェント][custom-agents]を学びました。チームの専門知識や標準を再利用可能なエージェントにまとめ、Copilot がより効果的に作業できるようにします。

このレッスンでは、次のことを行いました。

- カスタムエージェントの定義方法を学びました。
- タスクをカスタムエージェントに割り当てました。

Copilot がハイコントラストモードを実装している間に、次は mission control から[エージェントのセッションを監視して案内します][next-lesson]。

## リソース

- [カスタムエージェントについて][custom-agents]
- [組織でカスタムエージェントを使用する準備][org-custom-agents]
- [Enterprise でカスタムエージェントを使用する準備][enterprise-custom-agents]

---

| [← 前のレッスン: GitHub Copilot cloud agent][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
