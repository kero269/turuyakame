---
title: " Hugoでカテゴリをつくる"
date: 2022-09-02T09:20:13+09:00
draft: true
---

[HUGO でカテゴリ一覧を階層化する方法](https://aloha-ru.com/hugo/category-management/) ##　 Hugo の記事管理方法

- taxonomy
  > Taxonomy で管理する場合は、カテゴリーを複数セットして、カテゴリーの記述順通りに入れ子になるようにカテゴリ一覧のテンプレートを作る。この場合、格納フォルダは自由だけど、記述のブレがあるとそのまま採用されるのが欠点。
  > あと都度、カテゴリの入力が必要です。
- section
  > Section で管理する場合は、フォルダのある場所がそのままセクションになります。
  > フォルダの構造を変えたら URL が変わるけど、記事やセクションページごとにパーマリンクを指定しておけば問題ありません。
  > カテゴリの設定も不要です。

OK それではセクションにしようぞ。

はまりポイント

- 複数セクションをつくる場合は content 直下に置く
- トップページ（メインページ）に複数セクションを表示させたい場合は、`config`に指定する。
  ````
  [Params]
  mainSections = ["content", "daily", "tech"] # Specify section pages to show on home page and the "Recent articles" widget```
  ````
-