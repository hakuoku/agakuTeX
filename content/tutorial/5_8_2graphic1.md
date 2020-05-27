+++
title = ""
date = 2018-06-25T02:04:01+09:00
description = ""
slug = "5_8_2graphic1"
weight = 582
eyecatch = ""
topics = ["dvipdfmx", "graphicx"]
draft = true
[menu.toc]
    parent = ""
+++

&#x3000;dvipdfmxで使える画像フォーマットはPNG、JPEG、BMP、JPEG 2000、EPSです。これらの画像の読み込みには`\includegraphics`コマンドを使います。画像をTeX文書と同フォルダに置き、図を挿入したい箇所に`\includegraphics{ファイル名}`と書き込みます。

```LaTeX
\ruby{気息}{いき}で曇った汽車の窓ガラスへ、指で次のような、象形文字を丹念に書きつけた。
\includegraphics{fig47499_01.png}
　鹿皮の爪磨きで爪を磨きながら、ゆうゆうと十三世の動作を観察していたタヌは、
```

{{< figure src="/img/58graphic1/include.png" caption="" alt="画像の読み込み結果" class="" >}}

　90度回転した状態になってしまいました。これは元の画像の保存方法などの絡みもあるかと思われます。またサイズも少し大きすぎます。このあたりはオプションで変更できます。


#### 参考
- [dvipdfmx/画像のとりこみ - TeX Wiki](https://texwiki.texjp.org/?dvipdfmx%2F%E7%94%BB%E5%83%8F%E3%81%AE%E3%81%A8%E3%82%8A%E3%81%93%E3%81%BF)
- [LaTeXコマンド集 - 図の基本](http://www.latex-cmd.com/fig_tab/figure01.html)