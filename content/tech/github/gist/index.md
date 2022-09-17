---
title: "🧐 Gistとは何か〜どのように使うのかを試してみた"
date: 2022-09-17T16:33:43+09:00
url: "p/cqgud8q/"
archives: ["2022-09"] # !!!!!!
categories: [技術系] # fill in [example, test]
tags: [github] # fill in [example, test]
description: "私にとっては謎のサービスgistでfileを作ってみました。git cloneしてディレクトリを作り、ローカルからpushまで試しています。" # add description
summary: "私にとっては謎のサービスgistでfileを作ってみました。git cloneしてディレクトリを作り、ローカルからpushまで試しています。"
draft: false
---

名前は割とよく見るけど、一体何者なのかよくわからないサービス gist。さらに有用性もよくわかりません。ナニコレ。

しかし、hugo は shortcode を提供してくれています。hugo さんが推しているなら、きっとみんな使っているサービスに違いない…。だったら私も使いたい！と思い、調べてみました。

{{< toc >}}

## 🤔 gist って何?

そもそも gist って何?ってところから疑問なのですが、GitHub Docs には「すべての Gist は Git のリポジトリであり、フォークしたりクローンしたりできます。」とか書いてあって、全くわからん。ていうか、さらに疑問が巨大化。

いろいろみたところ、gist についてはこちら-> [HowToGist\.md](https://gist.github.com/t-nissie/9580883)が詳しいです。曰く gist とは、「ちょっとしたメモや短いコードをバージョン管理しながら公開するのに便利なツール」だそうで、clone してローカルで updete してから push もできちゃう、なんか悪くなさそうなツールです。メモやコードをいろんなところで活用するときには便利そう。

## 🛩 私の gist ページに飛んでみる

さっそく gist を使ってみます。github のアカウントがあれば`自分のアイコンをクリック>Your gist`で gist に飛べます。

驚いたことに、私の gist にはすでに 1 つのメモが存在していました。みると 9 年前に作ったらしい「心理学」というタイトルの、めちゃめちゃ長文のメモ…。一体 9 年前の私は何をしようとしていたのか。

9 年前の私って、gist の存在意義をぜんぜんわかってなかったんだなぁ。

そして私って昔から、新しいサービスに飛び付いては使わずに放置してきたんだなぁ…などと思いは遠い昔に戻ってしまいました。

## 🛠️ gist ファイルを作る

とか、昔に浸るのは大概にして、謎の「心理学」は残しておいたまま、新たに gist を作ることにしました。

ファイルを作るのはカンタンです。

- アイコンの左にある＋を押す
- 'Filename including extension..'に「ファイル名.拡張子」を入れる
- コードやメモを入力し'Create secret gist'あるいは'Create public gist'ボタンを押す

これでファイルができる訳で、普通の github のリポジトリと一緒で、embed したり clone したりができます。

hugo には shortcode があって、たとえば

```
https://gist.github.com/kero269/1089a6ef15dd1cb6eb1c5a33e13febd6
```

という gist であれば、

```html
{{</* gist kero269 1089a6ef15dd1cb6eb1c5a33e13febd6 */>}}
```

と記述すれば、こんな感じ ↓ に表示してくれます。

{{< gist kero269 1089a6ef15dd1cb6eb1c5a33e13febd6 >}}

## 📤 clone して updete して push する

[Gist の使い方のメモ · GitHub](https://gist.github.com/t-nissie/9580883)には、[git コマンドで手元に clone できる](https://gist.github.com/t-nissie/9580883#git%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%81%A7%E6%89%8B%E3%82%82%E3%81%A8%E3%81%ABclone%E3%81%A7%E3%81%8D%E3%82%8B)とあります。私もそれがやりたい 💨

clone したいディレクトリに移動して

```
git clone https://gist.github.com/1089a6ef15dd1cb6eb1c5a33e13febd6.git hugo
```

とすると`hugo`というディレクトリが作られている 🎉 中には、今つくった md ファイルも入ってます。このディレクトリに新しいファイルを追加したり変更したりして push すれば...

`Authentication failed`

…😞

Username と Password を入れろと言われるのですが、Username は gitHub と同じ、Password は**Personal access tokens**を入れなければなりません。ナニソレ 🔥

こちら->[GitHub Gist のリポジトリを Git ツールで運用したり他者と共同作業するための方法](https://monomonotech.jp/kurage/memo/m220316_githubgist_gittool.html)を参考に Personal access token をつくって push。

できた 🎉。

しかし、このやり方だと一つの gist の中に 2 つのファイルが入るという構造になってしまうんですよね。すなわち、ブログにも 2 つのファイルが掲載されてしまうのです。

そうか、それだと私が求める使い方には合わないなぁ…としょんぼり。ブログに掲載する場合は（私の場合は）、ひとつの gist にひとつのファイルというのが良さそうです。

やたらと時間をかけてしまった…😭 でも、git clone して、update して push できるようになったから良いのだ！と思うことにします。

## 🐸 まとめと感想

いままで謎だった gist というものを知ることができて良かったが、今後使うかは不明。
