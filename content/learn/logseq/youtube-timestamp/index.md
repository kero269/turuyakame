---
title: "📓 LogseqでYouTubeのタイムスタンプをつけたノートを取る"
date: 2022-09-19T17:57:06+09:00
url: "p/2af929s/"
archives: ["2022-09"] # !!!!!!
categories: [ツール] # fill in [example, test]
tags: [logseq] # fill in [example, test]
description: "Logseqなら、YouTube学習にとっても便利な、タイムスタンプをつけたメモが簡単に取れます。あたらしいことを学ぶとき、動画を活用することが多い私には嬉しい機能です。" # add description
summary: "Logseqなら、YouTube学習にとっても便利な、タイムスタンプをつけたメモが簡単に取れます。あたらしいことを学ぶとき、動画を活用することが多い私には嬉しい機能です。"
draft: false
---

Logseq なら、YouTube 学習にとっても便利な、タイムスタンプをつけたメモが簡単に取れます。あたらしいことを学ぶとき、動画を活用することが多い私には嬉しい機能です。

きっかけは、この tweet を見かけたこと。へぇぇぇ。そんなことできたんだぁ、と思った次第です。

{{< tweet user="xrawanx" id="1504392688300404740" >}}

Logseq に YouTube の動画を埋め込んで、`cmd+shift+Y`するとタイムスタンプが貼り付けられるらしいんですが、embed のやり方が間違っていて少しバタついてしまいました（<-私の理解力の問題）。

なんのことはない、logseq のコマンドを使って埋め込みをすれば良いだけの話でした。だから簡単。

## 🎹 埋め込んで「cmd+shift+Y」する

`/`とタイプして(logseq のコマンドを呼び出して)Embed Video URL を選択

![tk_20220919-181856.webp](tk_20220919-181856.webp)

URL を入力 ex.`{{video https://youtu.be/PvFr36bcpYc}}`

ノートを取りたい場所にカーソルを移して`cmd+shift+Y`(Windowsd では`Ctrl+Shift+Y`らしいのですが、mac しかないので試してません))
![tk_20220919-174833.webp](tk_20220919-174833.webp)

## 💇 Custom CSS に記述してみる

{{< youtube PvFr36bcpYc >}}
この動画の 07:01 ごろに、動画の表示サイズがなんかちっさいから`設定>custom css`で変えちゃいましょう！っていうところがあります。ちなみに私も変えました。高さはお好みでどうぞ。

```css
iframe[id^="youtube-player"] {
  height: 500px !important;
}
```

なお、私 🐸 は、ページでも項目でも、メタデータを入れておくのが好みです。理由は、query を使って整理する（される）ときに便利だから。よく使うものはテンプレートを作っておきます。

## 🐸 まとめと感想

この投稿の本題と関係ないんだけど、twitter の埋め込みをしたら、きっとまた Speed Insight の点数が下がるんだろうなぁ 😮‍💨。
