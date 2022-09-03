---
title: "URL Management"
date: 2022-09-02T20:43:35+09:00
draft: true
---

permlink を変えたい場合、[URL Management \| Hugo](https://gohugo.io/content-management/urls/)によれば`config`にルールを記述すれば良いとある。

そもそもセクションのつくり方として、content 直下に作らなければならないようだ。

[Content Sections \| Hugo](https://gohugo.io/content-management/sections/#nested-sections)

セクション（いままでの呼び名はカテゴリ）

[セクションテンプレート \(section\.html\) の中でセクションのタイトルを表示する \- まくまく Hugo ノート](https://maku77.github.io/hugo/layout/section-name.html)

## セクションはどう使うか問題

カテゴリもセクションも階層グループをもつという点は同じだが、
セクションごとにレイアウト（/layouts)を変えられる
セクションごとに投稿テンプレートを変えられる（/archetypes）
permalink に設定できる

どっちもできる

- リスト（コンテンツ一覧）をつくる

##　投稿で直接喜寿部する方法
