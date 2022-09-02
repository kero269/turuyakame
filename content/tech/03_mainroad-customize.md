---
title: "mainroad カスタマイズ"
date: 2022-09-02T11:01:34+09:00
draft: true
---

このページが詳しいかも　[Hugo \- Configuring Hugo](https://bwaycer.github.io/hugo_tutorial.hugo/overview/configuration/)

[Customization \- Mainroad](https://mainroad-demo.netlify.app/docs/customization/)

## パラメーター

### favicon.ico

[Newbie \- Favicon not showing \- HUGO](https://discourse.gohugo.io/t/newbie-favicon-not-showing/29406)

```config.toml
[params]
  favicon = "/img/favicon.ico"
```

### toc

toc: 記事内に目次を作成する場合は true。`config.toml`ではなく各投稿のマークダウンファイルでも設定できる。

## サマリーの長さ

デフォルトだと、サマリーがクソ長いです。短くしたい。

[Hugo によるブログ作成と mainroad テーマのカスタマイズ \- terashim\.com](https://terashim.com/posts/create-hugo-blog-and-customize-mainroad-theme/)

config.toml の最初の方（つまり[params]とかの上！）たとえば、languageCode の下とかに入れる。

```
# config.tomlに入れるんだよ〜。
hasCJKLanguage = true # 日本語・中国語・韓国語の単語カウントを有効にする
summaryLength = 120 # サマリーの長さを120単語にする
```

[Hugo のサマリーが大きすぎる件 \- awm\-Tech](https://blog.awm.jp/2016/01/02/hugo/)

[Hugo のサマリ長（Summary Length） · wshito's diary](http://diary.wshito.com/comp/cms/hugo-summarylength/)

## header

サイトヘッダーにカスタムロゴを設定できます。テキスト、画像、またはその両方を使用することができます。
注:ロゴ画像は、テキストと画像を同時に使用した場合、最大幅 128pixels × 最大高さ 128pixels で表示される。ここでのサイズ指定はできないっぽいので、画像の大きさを合わせて入れた。イメージは SVG にしたいところだが png…。

```config.toml
[Params.logo]
  image = "img/profile.png" #static/imgの中の"profile.png"
  title = "Mainroad"
  subtitle = "Just another site"
```

## thumbnail

デフォルトでは、サムネイル画像がリストと単一のページに同時に表示されます。 場合によっては、リストのようなページのサムネイルのみを表示し、単一のページに隠す(またはその逆)ことがあります。 設定によるグローバルサムネイルの可視性を制御するには、有効な値「リスト」と「ポスト」の組み合わせでキー可視性を使用します。 [Params.thumbnail] #リスト項目のみのサムネイルを表示する 可視性= ["リスト"]

## Sidebar

Mainroad comes with a configurable sidebar that can be on the left, on the right, or disabled. The default layout can be specified in the [Params.sidebar] section of the configuration. The position can be specified for home, list and single pages individually. Use the keys home, list and single with values "left", "right" or false.

mainroad にはサイドバーが、左側、右側、または無効に設定可能なサイドバーが付属している。サイドバーは、複数のウィジェットで構成されています。

- デフォルトのレイアウトは[Params]で指定できます。
- サイドバー]セクションを参照してください。
- 位置は、ホーム、リスト、およびシングルページに個別に指定できます。
- home キー、list キー、および single キーを「left」、「right」、または false のいずれかの値で使用します。
- ウィジェットの名前のリストを値として使用してウィジェットキーを使用して、ウィジェットを個別に使用するように設定することができます。
- テンプレートを layouts/partials/widgets/<name>.html の下に配置することで、独自のウィジェットを追加できます。
- ウィジェットのリストは、ページのフロントマターから上書きできます。

[Author] # Used in authorbox
name = "鶴屋蛙芽"
bio = "50 歳をとうに越えてしまった。"
avatar = "img/profile.PNG"

```config.toml
baseurl = "https://pokemori.itsys-tech.com/"
title = "ポケ森攻略まとめブログ"
DefaultContentLanguage = "ja"
languageCode = "ja-JP"
paginate = "10" # Number of posts per page
theme = "mainroad"
disqusShortname = "https-itsys-tech-com" # Enable Disqus comments by entering your Disqus shortname
googleAnalytics = "UA-XXXXXXXXX-X" # Enable Google Analytics by entering your tracking id

[Author] # Used in authorbox
  name = "いしぐろ すぐる"
  bio = "本サイトの管理人です。好きなキャラクターはジャックです。"
  avatar = "img/profile.PNG"

[Params]
  subtitle = "ポケ森ファンが発信するまとめサイト" # Deprecated in favor of .Site.Params.logo.subtitle
  description = "どうぶつの森ポケットキャンプのまとめサイトです。はじめたばかりのユーザーに役立つ攻略情報やプレイした感想などを発信しています。" # Site description. Used in meta description
  copyright = "いしぐろ すぐる" # Footer copyright holder, otherwise will use site title
  opengraph = true # Enable OpenGraph if true
  schema = true # Enable Schema
  twitter_cards = true # Enable Twitter Cards if true
  readmore = false # Show "Read more" button in list if true
  authorbox = true # Show authorbox at bottom of pages if true
  toc = true # Enable Table of Contents
  pager = true # Show pager navigation (prev/next links) at the bottom of pages if true
  post_meta = ["date", "categories"] # Order of post meta information
  mainSections = ["post"] # Specify section pages to show on home page and the "Recent articles" widget
  dateformat = "2006-01-02" # Change the format of dates
  mathjax = true # Enable MathJax
  mathjaxPath = "https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.6/MathJax.js" # Specify MathJax path
  mathjaxConfig = "TeX-AMS-MML_HTMLorMML" # Specify MathJax config
  highlightColor = "#009406" # Override highlight color
#   customCSS = ["css/custom.css"] # Include custom CSS files
#   customJS = ["js/custom.js"] # Include custom JS files

```
