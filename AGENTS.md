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
  - content/ja/: 日本語のページ本文と frontmatter
  - content/en/: 英語のページ本文と frontmatter。相対パスは日本語と同じにする
  - content/vi/: ベトナム語のページ本文と frontmatter。相対パスは日本語と同じにする
  - config/_default/: サイト設定
  - data/authors/me.yaml: 日本語の著者プロフィール
  - data/authors/me_en.yaml: 英語の肩書き、所属、学歴、経歴
  - data/authors/me_vi.yaml: ベトナム語の肩書き、所属、学歴、経歴
  - assets/css/custom.css: 追加スタイル
  - layouts/_partials/: カスタム表示ロジック
  - layouts/single.html: ニュース個別ページの日付表示
- 生成物で通常は編集しない:
  - public/
  - resources/_gen/
- サイト言語は日本語が既定:
  - config/_default/hugo.yaml の defaultContentLanguage は ja
  - 英語は /en/、ベトナム語は /vi/。defaultContentLanguageInSubdir は false

## Code Style

- Markdown frontmatter は YAML で記述する
- 日付は ISO 8601 形式 (例: 2026-03-18)
- 基本の authors は me を利用する
- 文字言語は日本語をデフォルトとする。英語ページの見える文字は英語にする
- 変更は最小限にし、既存の Hugo Blox ブロック構造を崩さない
- 頼まれない限り、論文の要旨、講演の summary と abstract は書かない
- 住所、電話番号、生年月日、会員番号、証明書番号は書かない

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
- 主要コンテンツ配置（ja と en で同じ相対パス）:
  - ホーム: content/ja/_index.md と content/en/_index.md
  - ニュース: content/ja/news/ と content/en/news/
  - 講演: content/ja/events/ と content/en/events/
  - プロジェクト: content/ja/projects/ と content/en/projects/
  - 論文: content/ja/publications/ と content/en/publications/
- 学歴カードは、上段が学位、下段が大学と研究科または学部と専攻
- 講演の見出しは日時と会場。著者は me のみ
- 学会の入会ニュースだけ date_precision: month を付ける。表示は 2006/01。ほかのニュースは年月日
- 「応募しました」の下書きは一覧に戻さない
- 本文、summary、abstract が空の論文・講演・ニュースはリンクにしない。noindex とサイトマップ除外のままにする
- 外部の作品ページがある講演は event_url を付け、一覧からはそこへリンクする
- 研究業績では me の名前を太字にする
- 関連プロジェクトには featured.png を置く。未公開のポスターやスライドは使わず、すでに公開されているページの画像を使う
- 要旨は頼まれない限り書かない

## Known Pitfalls

- publications のディレクトリ名は複数形が正:
  - 実体は content/ja/publications/ と content/en/publications/
  - .github/workflows/import-publications.yml は content/publication/ を参照しており不一致
- public/ はビルド出力のため、手動編集しても再生成で上書きされる
- ニュース一覧の view 名 news はテーマにない。date-title-summary を使う
- pnpm dev の実行中に新しいフォルダを足すと、ビルドログは成功しても URL が 404 のままになることがある。そのときは開発サーバーを止めて再起動する。既存ファイルの修正だけなら再起動は不要
- Netlify では hugo --gc --minify を使うため、ローカル差異確認時はこの差を考慮する

## Key Reference Files

- package.json
- netlify.toml
- config/_default/hugo.yaml
- config/_default/languages.yaml
- content/ja/_index.md
- content/en/_index.md
- data/authors/me.yaml
- data/authors/me_en.yaml
- .github/workflows/import-publications.yml
