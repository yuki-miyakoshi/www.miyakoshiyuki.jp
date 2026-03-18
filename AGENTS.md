# Project Guidelines

このリポジトリは Hugo Blox ベースの学術 CV サイトです。AI エージェントは以下を優先してください。

## Build and Test

- 依存関係インストール: pnpm install
- 開発サーバー: pnpm dev
- 本番ビルド: pnpm build
- 検索インデックスのみ再生成: pnpm run pagefind
- Hugo モジュール問題の復旧:
   - hugo mod clean
   - hugo mod get -u
   - hugo mod tidy

## Architecture

- 主な編集対象:
   - content/: ページ本文と frontmatter
   - config/_default/: サイト設定
   - data/authors/: 著者プロフィール
   - assets/css/custom.css: 追加スタイル
   - layouts/_partials/: カスタム表示ロジック
- 生成物で通常は編集しない:
   - public/
   - resources/_gen/
- サイト言語は日本語優先:
   - config/_default/hugo.yaml の defaultContentLanguage は ja
   - config/_default/languages.yaml の languageCode は ja-JP

## Code Style

- Markdown frontmatter は YAML で記述する
- 日付は ISO 8601 形式 (例: 2026-03-18)
- 基本の authors は me を利用する
- 文字言語は日本語をデフォルトとする
- 変更は最小限にし、既存の Hugo Blox ブロック構造を崩さない

### Frontmatter example

```yaml
---
title: "ページタイトル"
date: 2026-03-18
authors:
   - me
tags: []
---
```

## Conventions

- ニュース記事ファイル名は YYYYMMDD-XX.md を推奨
- 主要コンテンツ配置:
   - ニュース: content/news/
   - ブログ: content/blog/<slug>/index.md
   - 発表: content/events/<slug>/index.md
   - プロジェクト: content/projects/<slug>/index.md
   - 論文: content/publications/
- ホームのセクション構成は content/_index.md の sections を編集する

## Known Pitfalls

- publications のディレクトリ名は複数形が正:
   - 実体は content/publications/
   - .github/workflows/import-publications.yml は content/publication/ を参照しており不一致
- public/ はビルド出力のため、手動編集しても再生成で上書きされる
- Netlify では hugo --gc --minify を使うため、ローカル差異確認時はこの差を考慮する

## Key Reference Files

- package.json
- netlify.toml
- config/_default/hugo.yaml
- config/_default/languages.yaml
- content/_index.md
- data/authors/me.yaml
- .github/workflows/import-publications.yml
