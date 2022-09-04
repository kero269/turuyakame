---
title: "Hugoの投稿に画像を追加する"
date: 2022-09-02T10:17:15+09:00
draft: false
thumbnail: "img/placeholder.png"
---

{{< thumbnail src="IMG_8602.jpeg" >}}

## 記事の中でサムネイルを指定

[Customization \- Mainroad](https://mainroad-demo.netlify.app/docs/customization/)

Mainroad では、`config`および投稿のフロントマターでサムネイル表示の指定ができる。

```
#config.tomlの指定

[Params.thumbnail]
  visibility = ["list"] # Control thumbnail visibility
```

```
# 投稿.mdのフロントマター
thumbnail:
  src: "img/IMG_8602.jpeg"
  visibility:
    - list
    - post
```

thumbnail 画像の参照元は、`static/img`らしい。ページバンドルして、画像ファイル名だけを参照させようとしてもダメだった。

すべての記事に thumbnail をつけたいわけではないが、つける場合には`static/img`の中にサイズ調整した画像ファイルを放り込むことにする。なんか原始的だけど。

[ImageMagick – Convert, Edit, or Compose Digital Images](https://imagemagick.org/)を使って terminal からサイズ調整することにした。ちと面倒くさいので、プログラムにしたいところ。

## 記事内の画像に関する指定

### ショートコード

> Hugo は画像を表示するための組み込みショートコードとして figure を提供しています。 figure ショートコードの実装は、下記の GitHub リポジトリで参照できます。

[shortcodes/figure\.html \- Hugo](https://github.com/gohugoio/hugo/blob/aba2647c152ffff927f42523b77ee6651630cd67/tpl/tplimpl/embedded/templates/shortcodes/figure.html)

画像は`figure`(マークダウンの image syntakx 拡張)を使うと、[パラメーター](target="_blank")が使える。

{{< figure
src="frog_doushiyou2.png"
title="Screenshot"
class="center"
width="320"
height="640"
link="https://gohugo.io/content-management/shortcodes/#figure"
target="_blank"
alt="鶴屋蛙芽"
caption="これはキャプションです" >}}

[Shortcodes \| Hugo](https://gohugo.io/content-management/shortcodes/#figure)

Hugo 提供の`figure`も悪くはないが、記事内画像のほとんどは同一サイズにするから、もっと機械的にできるよう`Image Processing`を使ってショートコードをつくる。

[Image Processing \| Hugo](https://gohugo.io/content-management/image-processing/#page-resources)

[大きな画像ファイルから自動的に小さなサムネイル画像を生成する \(Image Processing\) \- まくまく Hugo ノート](https://maku77.github.io/hugo/misc/image-processing.html)

[hugo で画像を最適化して出力する \| tbsmcd\.net](https://tbsmcd.net/post/image_processing/)

## 画像リンクの変更

Markdown Render Hooks による解決方法
[Hugo で出力される a タグをカスタマイズする \- kamoqq\.info](https://kamoqq.info/post/hugo-render-hook-templates/)

[Hugo で permalinks を設定しているときの画像 URL の不具合と修正方法 \| 反面教師あり学習](https://blog.eqseqs.work/2021/05/15/133033/)
