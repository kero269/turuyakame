---
title: "Hugo のインストールからテーマまで"
date: 2022-09-02T09:01:34+09:00
draft: true
tags: [example, test]
categories: [tech]
---

- [Quick Start \| Hugo](https://gohugo.io/getting-started/quick-start/)
- ### Install Hugo
- ### Create a New Site
- ### Add a Theme
  - [Getting started \- Mainroad](https://mainroad-demo.netlify.app/docs/getting-started/)
  -
  ```terminal
  		  git submodule add https://github.com/vimux/mainroad.git themes/mainroad
  ```
  - `config.toml`に追加・変更
  -
  ```terminal
  		  echo theme = \"mainroad\" >> config.toml
  ```
  - [RSS Language Codes](https://www.rssboard.org/rss-language-codes)
  - 良さそうなテーマ
    - [All Tags \- DoIt](https://hugodoit.pages.dev/tags/)
    - [Neon Mirrors](https://neonmirrors.net/)
- ### Add Some Content
  -
  ```terminal
  		  hugo new posts/my-first-post.md
  ```
  - この時点では`draft: true`になっている。このままだとデポロイされない（ -> 次の Start the Hugo server をしてはじめて`draft: false`になる)
- ### Start the Hugo server

  -

  ```terminal
  		  hugo server -D

  		  # Ctrl+Cで止めるまでhttp://localhost:1313/ 上で状況を確認できる。
  ```

  - [Hugo でよく使うコマンド一覧 – Helve Tech Blog](https://helve-blog.com/posts/web-technology/hugo-commands/) > [hugo server option](https://helve-blog.com/posts/web-technology/hugo-commands/#オプション)
  - -D をつけるとドラフトまで表示してくれる。

- .gitignore を入れてしまおう。

  - [自分で\.gitignore を書く \- Qiita](https://qiita.com/gonta616/items/79e9728d71c19e8d2bab)
  - [\.gitignore の書き方 \- Qiita](https://qiita.com/inabe49/items/16ee3d9d1ce68daa9fff)
  - 内容は[gitignore/Hugo\.gitignore at main · github/gitignore](https://github.com/github/gitignore/blob/main/community/Golang/Hugo.gitignore)
  -

  ```.gitignore
  		  # Generated files by hugo
  		  /public/
  		  /resources/_gen/
  		  /assets/jsconfig.json
  		  hugo_stats.json

  		  # Executable may be added to repository
  		  hugo.exe
  		  hugo.darwin
  		  hugo.linux

  		  # Temporary lock file while building
  		  /.hugo_build.lock
  ```
