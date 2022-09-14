---
title: "😭 Xserverで作った独自ドメインのメールからgmailに送信できなかった件"
date: 2022-09-14T07:54:02+09:00
url: "p/wp73fxy/"
archives: ["2022-09"] # !!!!!!
categories: [技術系] # fill in [example, test]
tags: [Xserver] # fill in [example, test]
description: "他サーバで運用していた独自ドメインをXserverに移行し、併せてメールを作った。しかしgmail宛のメールだけ届かないという事態に陥ったが、アレコレやって解決しました。" # add description
summary: "他サーバで運用していた独自ドメインをXserverに移行し、併せてメールを作った。しかしgmail宛のメールだけ届かないという事態に陥ったが、アレコレやって解決しました。"
draft: false
---

他サーバで運用していた独自ドメインを Xserver に移行し、併せてメールを作ったところ、gmail アドレス宛のメールだけ届かないという事態に陥りました。

解決してみるとなんてこともない問題ではありましたが、やたらと時間がかかったのと、最後のハードルを作ったのは自分だったというオチが悲しくて、筆をとった次第です。

## 😩 問題：gmail 宛に送信すると daemon

gmail アドレス宛にメールを送信すると、あの有名な`mailer-daemon@`さんから"Undelivered Mail Returned to Sender"という件名のメールが届きました。久しぶりだな daemon....。

「あなたのメッセージは、1 人以上の受信者に届けられなかったことをお知らせしなければなりません。（I'm sorry to have to inform you that your message could not be delivered to one or more recipients. ）」からはじまるメールによると、私が送ったメールは「SPF を通過できなかった」そう。

```
The MAIL FROM domain [xxxx.xxx] has an SPF record with a hard
fail 550-5.7.26 policy (-all) but it fails to pass SPF checks
with the ip:550-5.7.26 [xxx.xx.xxx.xxx].
```

調べてみたところ、DNS TXT は Xserver 側のいうとおり**正しく登録されていた**。オンラインテスト[SPF Query Tool - kitterman](https://www.kitterman.com/spf/validate.html)を実施したところ、最初は「問題あり」っぽいお返事がかえってきましたが、**時間をおいてまた試したら**"Results - PASS sender SPF authorized"と成功しました。

- [DNS レコードの編集 \| レンタルサーバーならエックスサーバー](https://www.xserver.ne.jp/manual/man_domain_dns_setting.php)
- [間違いから学ぶ SPF レコードの正しい書き方 : 迷惑メール対策委員会](https://salt.iajapan.org/wpmu/anti_spam/admin/operation/information/spf_i01/)

この問題は、おそらくは、時間が解決した問題…。DNS 登録して間もない段階でメールテストを行ったため、SPF テストに通らなかっただけだと思います。**待つだけで良かった**のかもしれません。

## 😩 それでも送信できない〜ポート番号が違っていた

SMTP のポート番号が正しくなかった問題もありました。SSL 利用なので SMTP のポート番号を`465`にすべきところ`587`にしていたのです。

号泣 😭

これには理由があって、「Xserver gmail 宛 メール 送れない」などのキーワードで検索したときにあがってきたページに以下が記載されていたから、「`587`でいいんだ！」と思い込んでしまったのです…。ぐすん。

> 仕組みとしては難しいものですが、ユーザ側では、通常、お使いのメールソフトウェアで、送信用ポート（SMTP ポート）を、標準の 25 番ポートではなく、587 番へ設定をご変更いただくだけでご利用が可能となります。[OP25B について \| 法人向けレンタルサーバー【Xserver ビジネス】サポートサイト](https://support.xserver.ne.jp/manual/man_mail_op25b.php)

思い込み激しくない同僚が素直にポート番号を`465`に変更してくれて、「メール送れた〜」と連絡をくれました。ありがとう、おかげで、この問題に気づくことができたよ 🎉。

## 😩 Gmail にあるはずのメールが見えない

しかし、苦難はまだ続く。

自分用 gmail 宛に送っても、メールが'見えない'事態が続きました。エラーメッセージは来ないから、送信はできているはず。てことは、受信していない…? 神隠し 😱?

ふと思いついて、私が管理している他の gmail アドレスに送ってみました。すると、届いた 🎉。

えええ〜〜〜⁈と驚きつつ、**「受信トレイ」ではなく「すべてのメール」を確認**したら、大量の"test from オレ"メールが発見されたという次第です。

どうやら昔の私が、今回サーバー移行したメールアドレスについて gmail の自動振り分け機能を設定していたっぽい。すなわち、**「受信トレイをスキップして XXX というフォルダに入れる」的なフィルターをつけた**っぽい（そういえば、かすかに記憶…）。

自分のアドレス（今回移行したもの）から自分の gmail アドレスにメールを送ることがほとんどなかったため、すっかり忘れていました（ぐすん）。

ということで、めでたく解決しました。

## 🐸 まとめと感想

昔の私、余計なことすんな。
