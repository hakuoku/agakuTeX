+++
title = "割り注"
date = 2018-04-02T15:16:59+09:00
description = ""
slug = "5_7_4warichu"
weight = 574
topics = ["warichu"]
[menu.toc]
    parent = "footnote"
+++

{{< figure src="/img/57warichu/warichu.png" caption="" alt="割り注の例" class="" >}}

&#x3000;註にはもう一つ、本文の1行の中に小書きで2行の注釈を埋め込んだ割り注があります。これを実現するには[藤田眞作さん](http://xymtex.my.coocan.jp/fujitas/fujita.html)作の**warichu**パッケージが必要です。  
　こちらもTeX Liveには含まれていません。[配布ページ](http://xymtex.my.coocan.jp/fujitas2/texlatex/index.html)の中のwarichu.styをクリックしてダウンロードするか、あるいはパッケージ全文が表示されたらそれをコピーし、「warichu.sty」の名前で作業フォルダに保存してください。

　その上で`\usepackage{warichu}`すれば準備完了です。コマンドは、縦書き用の`\twarichu{注をつけたい箇所}{注本文}`です。この場合は以下のような感じですね。

```LaTeX
\twarichu{いささが}{いささがは原文ママ}空腹の模様でもある、
```

　ところがこの時、注本文の字数が奇数だと、なぜか2行目が組まれないという現象が起こります。

{{< figure src="/img/57warichu/odd.png" caption="" alt="2行目の欠けた割り注" class="" >}}

　ラディカルな解決法はちょっと見つからなかったので、小手先の方法に頼ります。つまり本文を無理矢理偶数にします。文を書き換えるか、適切な位置に全角スペースを一個挿入してください。一番上の画像は「が」と「は」の間に手でスペースを入れたものです。

　トータルの字数を偶数にすれば、このようにきちんと組んでくれます。

{{< figure src="/img/57warichu/even.png" caption="" alt="4文字の割り注" class="" >}}

### 位置の修正
　画像を見て気づいたかと思いますが、この割り注、フォントサイズによっては中心からずれてしまいます。修正方法はwarichu.styを書き換えることです。192行目からを以下のように書き換えてください。

```LaTeX
\newdimen\twari@tbaselineshift
{\warisize \let\twari@tbaselineshift=\tbaselineshift%
\dimen3=\ht2 \divide\dimen3 by2
\dimen4=\dimen3
\advance\dimen3 by.65\twari@tbaselineshift
\advance\dimen3 by-.0zw
\advance\dimen4 by-.65\twari@tbaselineshift
\advance\dimen4 by.0zw
\dp2=\dimen4\ht2=\dimen3\box2}}%
```

{{< figure src="/img/57warichu/aligned.png" caption="" alt="位置の修正完了" class="" >}}

#### 参考
- [QA: warichu.sty](https://oku.edu.mie-u.ac.jp/tex/mod/forum/discuss.php?d=1278)