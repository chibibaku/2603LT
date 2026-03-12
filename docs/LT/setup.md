---
title: LT大会用 セットアップガイド
date: 2026-03-10
---

# LT大会用 セットアップガイド 


[[toc]]

## 前提条件
- git, gh, nodeが入っている
- GitHubのアカウントがある
- cloudflareのアカウントがある(オプション)

## vitepressを入れる
```
git init
npm install vitepress
```

## .gitignoreを書く
```
# Node files
node_modules/
package-lock.json

# vitepress outputs
docs/.vitepress/dist/
docs/.vitepress/cache/
```

node関連のファイルとvitepressのビルド・キャッシュがGitHubに飛ばないようにする

## GitHub Actionsでワークフローを組む
GitHub Pagesに自動でデプロイするためのワークフローを組む

::: details GitHub Actionsのワークフロー例 ( `.github/workflows/deploy.yml` )
```
name: Deploy VitePress to GitHub Pages

on:
  push:
    branches:
      - main

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-slim
    strategy:
      matrix:
        node-version: [20]
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        
      - name: Install pnpm
        uses: pnpm/action-setup@v4
        with:
          version: 10

      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}

      - name: Install dependencies
        run: pnpm install

      - name: Build
        run: pnpm docs:build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: docs/.vitepress/dist

  deploy:
    needs: build
    runs-on: ubuntu-slim
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```
:::

## Gitリポジトリ & GitHubにRepo立ててpushする
```
gh repo create [rpeo名] --[private/public]
git init
git branch -M main
git add .
git commit -m "First commit"
git remote add origin https://github.com/[ユーザー名]/[repo名]
git push origin main
```

## GitHub Pages用の設定をする
- GitHubのリポジトリのSettings > Pagesに行く
- SourceをGitHub Actionsのビルドで生成されるブランチにする
- config.mtsのbaseをリポジトリ名にする
  ```
  export default defineConfig({
    base: '/2603_LT/',
    // ...
  ```

<!-- ## Cloudflare Pages (スライドでは紹介しない部分)
docs/.vitepress/dist

| Configuration option | Value |
| --- | --- |
| Production branch | main |
| Build command | npx vitepress build |
| Build directory | .vitepress/dist |


https://dash.cloudflare.com/?to=/:account/workers-and-pages -->