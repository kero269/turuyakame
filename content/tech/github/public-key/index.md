---
title: "😭 githubへのpushが'Permission denied (publickey)'されたが解決した話"
date: 2022-09-13T10:09:41+09:00
url: "p/famfdf2/"
archives: ["2022-09"] # !!!!!!
categories: [技術系] # fill in [example, test]
tags: [github, エラー] # fill in [example, test]
description: "githubへのpushが'Permission denied (publickey)'されましたが、SSHキーを登録しgithubに追加したことで解決できました。" # add description
summary: "githubへのpushが'Permission denied (publickey)'されましたが、SSHキーを登録しgithubに追加したことで解決できました。"
draft: false
---

本ブログに[Google アナリティクス](https://analytics.google.com)を入れたんで、github に push しようとしたら冷たく拒絶されました。

```
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.
```

「なによ〜😭 "fatal（致命的）"とか怖い 😭😭」と焦りつつ調べてみたら、どうやら「鍵」に問題があるらしい。まぁ確かに、エラーメッセージにも`(publickey)`と明記されていることだし、そうなのでしょう。

とはいえ。最後の push は一昨日だし、その後に鍵をなくすような何かをした覚えはない…。とはいえ、拒絶されている以上どうにかするしかありません。

ちなみに今回のお話は、macBook Pro、macOs Monterey(version: 12.5.1)という環境で terminal を使って行いました。

## 👷‍♀️ 実施した作業

### 1. ssh で github にアクセスできるか確認

```
$ ssh -T git@github.com
```

-> `git@github.com: Permission denied (publickey).`。またもや拒絶されました。

### 2. デバックログを確認

上のコードに v をつけるとデバックログが出力されます。なのでそれを確認します。

```
$ ssh -vT git@github.com
```

だーっとログが出てきますが、必要なのは`identity file`のところです。なので`identity`を検索して該当するログに飛んでみます。すると、「~/.ssh/鍵ファイルが認識されていない」というメッセージがありました（下記参照）。ファイル名の後に[-1]と記述されているなら、ファイルがないとか認識できないとかそんな感じ。

```
debug1: identity file /Users/私のフォルダ名/.ssh/id_rsa type -1
```

この記述以下、全部で 14 メッセージありました。ということは、github さんは 14 回試行したけど該当するものは一個もなかった、だから「あくせすでないど！」となったのでしょう…。github お疲れさま。

### 3. 秘密鍵が~/.ssh/にあるのか確認

```
$ ls -al ~/.ssh
```

と入れるとなんか出てくるけど、上記に該当するもの（たとえば id_rsa）は 1 つもない。ということは、鍵を作らなければ…。

参考: [既存の SSH キーの確認 \- GitHub Docs](https://docs.github.com/ja/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)

### 4. 新しい SSH キーの生成

[新しい SSH キーを生成して ssh\-agent に追加する \- GitHub Docs](https://docs.github.com/ja/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)のとおりにやりました。「新しい SSH キーを生成する」-> 「SSH キーを ssh-agent に追加する」までやって、[GitHub アカウントへの新しい SSH キーの追加 \- GitHub Docs](https://docs.github.com/ja/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)に進みます。

### 5. アカウントへの新しい SSH キーの追加

公開キーをクリップボードにコピーします。この例では`id_ed25519.pub`をコピーしていますが、もし他の鍵ファイルをコピーする場合は、該当ファイル名に変更します（例：~/.ssh/id_rsa.pub）。

```
$ pbcopy < ~/.ssh/id_ed25519.pub
```

これを github の自分のアカウントの「設定> **SSH キーと GPG キー**」に入って追加します。詳細は[GitHub アカウントへの新しい SSH キーの追加 \- GitHub Docs](https://docs.github.com/ja/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)のとおり。

Key を入れる窓でペースト(ctrl+v）して、`Add SSH Key`ボタンをクリック!

したのですが、`git push ~~`しても拒否されてしまいました。なぜ 😭?

なので、一度 github の鍵の登録を削除して、もう一度「公開キーのコピー」と「キーの追加」の手順を繰り返しました。

2 度めはあっさり通過。何が良かったのか悪かったのかわからないのですが、**コピーがちゃんとできていなかった**とか、あるいは**キーを追加したときに無駄なスペースか改行を入れてしまった**とか、そういうミスだと思います。割とよくやるから。

## 🐸 まとめと感想

鍵がなくなると面倒になることになるのは、現実社会と同じ。でも、コンピューターの世界では、鍛冶屋に頼まずとも鍵が作れるのは素晴らしいですね。

それにしても、一昨日まで使っていた鍵はどこに行ったの?
