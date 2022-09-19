---
title: "🎉 Hugoサイトを構造化データ(JSON-LD)対応にした"
date: 2022-09-15T17:11:15+09:00
url: "p/etjzggy/"
archives: ["2022-09"] # !!!!!!
categories: [技術系] # fill in [example, test]
tags: [hugo, google] # fill in [example, test]
description: "本サイトを構造化データ対応にしました。また、フロントマターを参照できるようになりました。Yeah!" # add description
summary: "本サイトを構造化データ対応にしました。また、フロントマターを参照できるようになりました。Yeah!"
draft: false
---

本サイトを構造化データ対応にしました。うふふ 🤗

なお、構造化データができたことも嬉しいのですが、フロントマターを参照できるようになったことが、とても嬉しい。

{{< toc >}}

## 🤔 構造化データとは

> 構造化データとは、ページに関する情報を提供し、そのコンテンツ（たとえば、レシピページの場合は材料、加熱時間と加熱温度、カロリーなど）を分類するために標準化されたデータ形式です。
>
> [構造化データマークアップとは \| Google 検索セントラル  \|  ドキュメント  \|  Google Developers](https://developers.google.com/search/docs/advanced/structured-data/intro-structured-data)）

データ形式について Google は[JSON-LD](https://json-ld.org)を推奨しています。

構造化データに対応すると、Google の検索に強くなる（コンテンツが把握されやすくなる）、レシピや How-to やニュースなどは、検索結果の上の方にカード形式で表示される可能性も高まるのだとか。

世の中の情報はこうして枠にはめられていくんですね。それでは、積極的に枠にハマりに行きましょう！

## 🚧 構造化データ対応のためにしたこと

構造化データ対応のために私は、以下の作業をいたしました。

1. 自分のコンテンツに当てはまるデータ形式をつくって`layout/partial/schema.html`として保存
2. 自分のサイトに埋め込む
3. 自動で取得して欲しい箇所は サイト内の情報を参照するように記述を変更

### 1. 自分のコンテンツに当てはまるデータ形式をつくる

まずは、`layout/partial/schema.html`をつくっておきます。

そしてそこに[JSON\-LD \- JSON for Linking Data](https://json-ld.org/)形式のデータを入れ込みます。

今回は、情報を箇所を入力すれば JSON-LD 形式に変えてくれるオンラインツール（[Schema Markup Generator \(JSON\-LD\) \| TechnicalSEO\.com](https://technicalseo.com/tools/schema-markup-generator/)）を使います。必要な情報を入力欄に入れると、スクリプトとして書き出されるのでこれをコピーし、`layout/partial/schema.html`にペタリ。

必要な情報って何…?と思った場合は、下記私の実例を参考に適当に入れてみてください。

```layout/partial/schema.html

# layout/partial/schema.html

<script type="application/ld+json">
{
    "@context": "https://schema.org",
    "@type": "Article",
    "headline": "Hugoの投稿に画像を追加する",
    "image": [
    "img/thumbnail/680-tk_20220906-134844.webp",
    "../img/og-image.jpg"
],
    "author": {
    "@type": "Person",
    "name": "鶴屋蛙芽"
    },
    "publisher": {
    "@type": "Organization",
    "name": "鶴屋蛙芽ブログ",
    "logo": {
        "@type": "ImageObject",
        "url": "img/kame_logo.svg"
    }
    },
    "datePublished": "2022-09-02 10:17:15 \u002b0900 JST",
    "dateModified": "2022-09-02 10:17:15 \u002b0900 JST"
}
</script>
```

### 2. 自分のサイトに埋め込む

`layout/partial/schema.html`を header か body で読み込みます。

私は `layout/partials/header.html`に入れました(theme: meinroad)。

```layout/partials/header.html
<head>
...
...
{{- partial "schema.html" . -}}
</head>

```

この時点で「4. 構造化データをテスト」してみても良いかも。私はやってないけど。

### 3. サイトの情報を参照するように記述を変更

`layout/partial/schema.html`の記述のままだと、たとえば個別投稿の URL などの動的に変わって欲しい箇所が固定されたままになってしまいます。

なので、置き換えられる箇所は hugo の front matter を参照しにいくように記述を変更します。

[コンフィグファイルに設定した情報を参照する \- まくまく Hugo ノート](https://maku77.github.io/hugo/settings/read-config.html)を参考に`config.toml`する記述を入れ、[ショートコードの中からフロントマターのパラメータを参照する \($\.Page\.Params\) \- まくまく Hugo ノート](https://maku77.github.io/hugo/shortcode/frontmatter-params.html)を参考に各投稿の title と image を参照する記述を入れました。

```layout/partial/schema.html
# layout/partial/schema.html

<script type="application/ld+json">
{
    "@context": "https://schema.org",
    "@type": "Article",
    "headline": "{{ .Title }}",
    "image": [
    {{ .Page.Params.thumbnail }},
    "../img/og-image.jpg"
],
    "author": {
    "@type": "Person",
    "name": {{ .Site.Author.name }}
    },
    "publisher": {
    "@type": "Organization",
    "name": "{{ .Site.Title }}",
    "logo": {
        "@type": "ImageObject",
        "url": {{ .Site.Params.logo.image }}
    }
    },
    "datePublished": "{{ .Date }}",
    "dateModified": "{{ .Lastmod }}"
}
</script>
```

6 行目で image を指定するとき、第 1 候補(各投稿の thumbnail)と第 2 候補（config.toml で指定した OGP）になるようにしています。私は thumbnail を index.md のフロントマターで指定しているのでこういう記述になりました。

ご本家[Site Variables \| Hugo](https://gohugo.io/variables/site/)もぜひ確認してね。

### 4. 構造化データをテスト

[構造化データマークアップをテストする \| Google 検索セントラル  \|  Google Developers](https://developers.google.com/search/docs/advanced/structured-data)に記載されている下記テストでチェックします。
[リッチリザルト テスト \- Google Search Console](https://search.google.com/test/rich-results)
[スキーマ マークアップ検証ツール](https://validator.schema.org/)
うまくいくと「● 件の有効なアイテムを検出しました」というメッセージが、問題があるとエラーメッセージが出ます。たとえば変な文字が入ってしまった場合（syntax error）などの場合は「構文にエラーがある構造化データが検出されました」などと警告されます。

## 🐸 まとめと感想

構造化データにして良いことがあるのかわからないけれど、一応できたっぽいので良かったです。最大の収穫は、いまいちわかっていなかった参照の方法がわかったことです〜🤗
