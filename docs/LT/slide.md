---
marp: true
theme: default
paginate: false
header: ''
footer: ''
backgroundColor: White
color: Black
size: 4:3
_class: lead
---

<!-- タイトルページ -->
# GitHub Actions+VitePressで<br/>読み返しやすいメモを取る

---

# 1. 導入 / 目的

---

## メモを"読み返す"価値と課題
- メモは書くだけでなく、読み返すことに価値がある
- AgentやObisidianの台頭で、メモの活用方法が変化
- Twitter以上, Qiita未満のメモのニーズ
- Zenn (Zenn Cli)やGistとも違う、個人用のメモの位置づけ

---

## GitHub Actions＋VitePressを使う理由
- デプロイの自動化で手間を減らす
- Markdownで書けるので手軽
- ローカルファイルと同じ階層構造
- デザインテーマや設定のノウハウが多い
- Vite譲りの性能と記事特化の機能性

---

# 2. 基本概念

---

## VitePressとは
``https://vitepress.dev/``
- VitePressはMarkdownを高速にHTMLに変換し静的サイトを生成するツール

---

## GitHub Actionsとは
``https://github.com/features/actions?locale=ja``
- GitHubのCI/CDサービス
- repo内でワークフローを定義
- トリガーで実行でビルド・テスト・デプロイなどのタスクを自動化

---

# 3. ワークフロー全体像

---

## リポジトリとフォルダ構成

 → いたって普通のnodeプロジェクトの構成
```
my-memo-repo/              // リポジトリルート
├── .github/
│   └── workflows/
│       └── deploy.yml     // GitHub Actionsのワークフロー定義
├── docs/
│   ├── .vitepress/
│   │   └── config.mts     // VitePressの設定
│   ├── index.md           // トップページ
│   ├── ...                // メモ・記事のMarkdownファイル
├── node_modules/
├── .gitignore
└── package.json
```
vitepressのドキュメントルートは`docs/`に設定すると、既存のプロジェクトに組み込みやすい

---

## 編集→コミット→CI→公開の流れ図

| | 場所 | 内容 |
|----------|------|------|
| 1 | ローカル | VitePressプロジェクトを構築 |
| 2 | ローカル | Markdownでメモを書く |
| 3 | GitHub | 変更をコミット＆プッシュ |
| 4 | GitHub<br>Actions | ワークフローを自動トリガー<br>ビルドとデプロイが実行される |
| 5 | Web | 公開されたサイトにアクセス |

---

## deploy.ymlの例
```yaml

```

---

# 6. Tips / ベストプラクティス

---

## 出力結果を見やすくする工夫
- 目次の表示

---

## 出力結果を見やすくする工夫
- アラート・カスタムコンテナ配置

---

## 出力結果を見やすくする工夫
- コードブロック

---

## 出力結果を見やすくする工夫
- mathjax統合

---

# 7. まとめ・Q&A

---

## まとめ
- GitHub ActionsとVitePressでメモを公開するメリットを再確認

---

## 質疑応答
- 何か質問があればどうぞ

## 連絡先
