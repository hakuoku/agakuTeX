+++
title = "note：ドライバ"
date = 2018-06-24T20:48:33+09:00
description = ""
slug = "5_8_1driver"
weight = 581
eyecatch = "/img/58driver/ptex2pdf.png"
topics = ["graphicx", "dvipdfmx"]
[menu.toc]
    parent = "graphics"
+++

&#x3000;大事な大事な画像の処理です。画像を読み込むためには**graphicx**パッケージを使います。

```LaTeX
\usepackage{graphicx}
```

　早速使い方の説明に行きたいところなのですが、実はgraphicxパッケージはこれだけでは**動きません**。試しに画像を同フォルダに置いて、`\includegraphics{画像名}`コマンドを入れてコンパイルしてみると、こんなエラーが出ます。

```
LaTeX Error: Cannot determine size of graphic in fig47499_01.png (no Bounding Box).
```

　これはgraphicxパッケージが**ドライバ依存性**を持つためです。ドライバとは何ぞやと言いますとこれは**dviドライバ**の略で、dviファイルをPDFに変換するソフトのことです。  
　そもそも素のTeX（この場合はupLaTeX）は、PDFを作るソフトではありません。dviという中間ファイルを吐き出すソフトウェアです[^1]。これをPDFに変換するためにドライバが必要になります。  
　日本でよく使われるのは**dvipdfmx**というドライバです。TeXWorksでupLaTeXを選ぶと、後ろにカッコで（ptex2pdf）というのがついています。

{{< figure src="/img/58driver/ptex2pdf.png" caption="" alt="TeXWorksの表示" class="" >}}

　これはupLaTeXなどのTeX本体に続けてdvipdfmxを起動してくれるスクリプトです。エンジンを選ぶとTeXWorks側で自動的にドライバを呼び出してくれるんですね。  
　というわけでこれまで我々はupLaTeX+dvipdfmxを使ってきました。パッケージがドライバ依存性を持つということは、TeX文書の中で使っているドライバを明示的に指定してやる必要があるということです。  
　具体的にはパッケージオプションに`[dvipdfmx]`と書いてやります。この時graphicxパッケージのオプションに書いてやってもいいんですが、TeXには他にもドライバ依存を持つパッケージがあります。その度にパッケージオプションに書いてやるのは手間ですし想定外の動作の元になる可能性がありますので、オプションは1行目のドキュメントクラスのところにグローバルに入れてやるのが正しい書き方です。  

```LaTeX
\documentclass[uplatex,dvipdfmx]{utbook}
```

　これでgraphicxパッケージが使えるようになりました。次項から具体的な画像の読み込みについて説明します。

#### 参考
- [ptex2pdf - TeX Wiki](https://texwiki.texjp.org/?ptex2pdf)
- [graphicx - TeX Wiki](https://texwiki.texjp.org/?graphicx)
- [LaTeX の「アレなデフォルト」 傾向と対策 - Qiita](https://qiita.com/zr_tex8r/items/297154ca924749e62471)

[^1]: ただし最近はpdfTeXなど、直にPDFを出してくれる拡張もある。欧米ではこちらの方が主流になりつつあるが日本語組版には向かない。