+++
title = "はじめに"
date = "2018-01-19T14:28:23+09:00"
description = ""
slug = "4_4_0punct"
weight = 440
lastmod = "2018-01-27T15:47:27+09:00"
topics = ["パッケージ"]
[menu.toc]
    parent = "punctuation"
+++

&#x3000;英数字・記号まわりの制御が終わりましたので、今度は日本語・縦書きならではの約物（[Wikipedia](https://ja.wikipedia.org/wiki/%E7%B4%84%E7%89%A9)）の処理に入ります。現時点ではこんな問題点があります。

- フォントによってダッシュ――の真ん中に隙間が空いてしまう
- 引用符の表示がおかしい
- ！や!?の後に空白が入らない etc.

　このうちいくつかの問題は、ZRさんの書いて下さったミニパッケージを使うことで解決できます（多謝）。  
　[LaTeX： 和文を欧文扱いして和文扱いする件](https://gist.github.com/zr-tex8r/e945f3a7d3c7b775cbc3edc96d63ea8b)

　これをさらに改良したものが[こちら](https://gist.github.com/hakuoku/188b761d7904016f7ab831ffc9f4d50a)です。リンク先のGistのページの右上の「Download ZIP」ボタンを押してzipフォルダをダウンロードしてください。解凍してできたフォルダの中の「zrjapunct1.sty」を組版している作業フォルダに移し、あとは普通にプリアンブルで`\usepackage{zrjapunct1}`を宣言します。 （**pxcjkcatパッケージの後で**読み込んでください）  
　TeX Liveに含まれていないパッケージは、こんなふうに.styファイルを組版したい文書と同じフォルダに置くことで使えるようになりますので覚えておいてください。

　次項からはそれぞれの約物の詳しい挙動を説明していきます。