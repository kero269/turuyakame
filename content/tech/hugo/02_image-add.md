---
title: "Hugoの投稿に画像を追加する"
date: 2022-09-02T10:17:15+09:00
draft: false
thumbnail:
  src: "https://tiny-trifle-b4e820.netlify.app/posts/tech/IMG_8602.jpeg"
  visibility:
    - list
    - post
---

## Page Resources のはなし

[Image Processing \| Hugo](https://gohugo.io/content-management/image-processing/#page-resources)

画像は`figure`(マークダウンの image syntakx 拡張)を使うと、[パラメーター](target="_blank")が使える。

{{< figure
src="kame_logo2.png"
title="Screenshot"
class="center"
width="320"
height="640"
link="https://gohugo.io/content-management/shortcodes/#figure"
target="_blank"
alt="鶴屋蛙芽"
caption="これはキャプションです" >}}

[Shortcodes \| Hugo](https://gohugo.io/content-management/shortcodes/#figure)

## ショートコードを作成する

> Hugo は画像を表示するための組み込みショートコードとして figure を提供しています。 figure ショートコードの実装は、下記の GitHub リポジトリで参照できます。

[shortcodes/figure\.html \- Hugo](https://github.com/gohugoio/hugo/blob/aba2647c152ffff927f42523b77ee6651630cd67/tpl/tplimpl/embedded/templates/shortcodes/figure.html)

## 記事の中でサムネイルを指定

[Customization \- Mainroad](https://mainroad-demo.netlify.app/docs/customization/)

```
thumbnailImage: //localhost:1313/posts/2022/0902/.png
```

> これはサムネイルの指定になります。下記の記載はローカルで確認するために localhost:1313 になっていますが、実際にデプロイする際はブログのドメインを指定してください。トップページを見てみると以下のようにサムネイルが表示されていますね。

[hugo を使った爆速ブログをカスタマイズする](https://zenn.dev/harachan/articles/21d8f3a9f2ca4e)

投稿の md ファイル

```
thumbnail:
  src: "//localhost:1313/posts/2022/0902/IMG_8602.jpeg"
  visibility:
    - list
    - post
```

## 大きな画像から小さなサムネイル画像を生成

[大きな画像ファイルから自動的に小さなサムネイル画像を生成する \(Image Processing\) \- まくまく Hugo ノート](https://maku77.github.io/hugo/misc/image-processing.html)
