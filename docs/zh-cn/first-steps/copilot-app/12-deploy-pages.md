---
title: "第 12 课 - 使用 GitHub Pages 部署网站"
description: "使用 GitHub Copilot app 配置 Pages 工作流，审查其拉取请求，并验证线上版 Space Quiz。"
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

使用 GitHub Pages 为 Space Quiz 提供公开访问地址。Copilot 可以准备工作流并指导部署，但你仍需负责审查更改并确认网站已上线。

本课将介绍如何：

- 请 Copilot 配置 GitHub Pages 部署。
- 在合并前审查工作流和拉取请求。
- 跟踪部署并验证已发布的网站。

## 场景

Space Quiz 已位于 GitHub 存储库中，但人们仍需要一种简单方式来试用。通过 GitHub Pages 发布这个单文件网站，用户可直接通过公开 URL 访问，无需添加服务器或运行时依赖。

## 请 Copilot 准备部署

> [!WARNING]
> 创建拉取请求可能会提交并推送代码。在发送以下提示词前，请审查批准设置和目标存储库。启用 **Approve all** 后，可能不会再出现单独确认提示。

在 `space-quiz` 的 Copilot app 会话中发送以下提示词：

```plaintext
Prepare a GitHub Pages deployment for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages after changes reach the default branch. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and report its link and any required Pages settings or permissions. Do not merge, enable auto-merge, change Pages settings, or deploy. Stop and wait for my review.
```

## 审查工作流和拉取请求

1. 确认 README 仅在存储库尚未提供时才会添加。
2. 审查拉取请求中的更改，包括工作流的构建与部署步骤、触发条件和权限。
3. 确认工作流从默认分支部署，而不是从未合并的拉取请求部署。
4. 请求必要的修正并审查更新后的差异。授权合并前，等待必需的拉取请求检查通过。

## 授权合并和部署

> [!WARNING]
> 以下提示词授权智能体合并已审查的拉取请求、修改存储库的 Pages 设置并发布网站。仅在完成审查，并确认存储库和拉取请求无误后发送。批准设置可能允许智能体执行这些操作，而不再发出另一条确认提示。

将 `<PR_NUMBER>` 替换为你审查过的拉取请求编号，然后发送这条单独提示词：

```plaintext
I have reviewed pull request <PR_NUMBER> in this repository and authorize its merge and deployment. Enable GitHub Pages using GitHub Actions, merge that pull request only after required checks pass, and monitor the deployment until it succeeds. Report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
```

![三阶段示意图：已合并的 space-quiz 拉取请求；成功运行的 GitHub Actions Deploy website，其中包含 Build website、Upload artifact 和 Deploy to Pages 步骤；以及位于 yourname.github.io/space-quiz/ 的线上版 Space Quiz。](../../../_images/first-steps-app-pages-deploy.svg)

## 验证部署

1. 持续跟踪 GitHub Actions 部署运行，直到其成功。
2. 打开报告的 URL，并确认 Space Quiz 已加载。

如果智能体无法启用 Pages 或合并拉取请求，请按其提供的具体说明操作。在部署成功且线上网站加载完成之前，不要将任务视为完成。

## 总结与后续步骤

现在，Space Quiz 已作为线上网站开放，你已通过实际验证确认部署成功，而不是仅依赖智能体的报告。继续学习[第 13 课：审查与后续步骤][next-lesson]。

[next-lesson]: ../13-review/
