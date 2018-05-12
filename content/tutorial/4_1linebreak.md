+++
title = "改行・段落"
date = "2017-04-22T19:24:51+09:00"
description = ""
topics = ["プリアンブル", "マクロ", "コメント", "obeylines", "xobeylines"]
slug = "4_1linebreak"
weight = 410
lastmod = "2018-05-11T17:31:44+09:00"
[menu.toc]
    parent = "edit"
+++
&#x3000;それにしても読みづらいですね。改行が全然なくて一面に字が植えてある。**面倒なことにTeXは、いわゆる普通の改行を感知しません。**  
　いやさすがに語弊があるな。正しくは下のように、間に空行を入れることで改行、つまり新たな段落が製造されます。

{{< figure src="/img/41linebreak/kuugyou.png" caption="" alt="新しい段落" class="" >}}

　じゃあ改行したいところに空行を入れていけばいいのかとなると、そうとも言い切れません。だってこうなるんだよ。（十蘭は改行少ないので乱歩で）

{{< figure src="/img/41linebreak/rampo.png" caption="" alt="行間の空きすぎた乱歩" class="" >}}

　いやだ！こんなの乱歩じゃない！なにより面倒くさい。いちいち空きを入れてくなんてミスも増えそうだし。  
　間が開かない段落内強制改行のやり方は、[一般的](http://www.latex-cmd.com/struct/space.html)には行末に`\\`か`\newline`を入れることです。ただこれも、面倒くささとミスのしやすさでは大して変わりません。

　もともと英語の特に論文では、新しい行＝新しい段落という認識なので、空行方式で破綻なく書いて組版できます。でも小説でいうと、改行って必ずしも新しい段落に移るわけじゃないですよね。特にセリフがそうで、会話になると改行のオンパレードだけど段落は全部一緒です。  
　この改行・段落問題はMarkdownなどとも共通で、個人的にはかなり根深い問題だと思っています。単なる英語と日本語の壁かと思ったんですが、機械にとっての解析のしやすさや伝統的な組版ルールとの絡みなどもあり、また英語圏でも空行派vs反対派議論は存在するようです。[^1]  
　というわけでここでは正しい文法を模索するよりも、.texファイルの扱いやすさおよび表現としての柔軟さを重視します。たとえ段落と強制改行を使い分けてきちんと整形した正しいTeX文書でも、エディタでファイルを開いた時に行の間がスカスカだと腹が立ってくるからです。編集作業は楽しくやりたい。

　そのためにはあらかじめこちら側で、「全部の行を見たまま改行する」的なコマンドを指定しなければなりません。TeXにはもともと`\obeylines`というコマンドがあって、これを書いてやると大体望む動作になります。  
　エスケープの時のような部分的なコマンドではない、文書全体に関わるコマンドは本文が始まる前、`\documentclass`と`\begin`の間で指定します。ここの間のことを**プリアンブル**といいます。以降のコード例ではプリアンブルの部分のみを示していることがあります。  
　これでちゃんと改行できたかのように見えるんですが、実はまだ落とし穴があります。

{{< figure src="/img/41linebreak/obeylines.png" caption="" alt="空行が反映されない" class="" >}}

　**空きが反映されてない。**実はobeylinesは、「 _文字のない空白だけの行は無視する_ 」というTeX本来の動作に従います。なので一行アキや二行アキを入れたくて何回改行しても無視されます。  
　空行の制御には\vspaceコマンドなどがあるんですが、本文が読みづらくなるのであまり使いたくありません。どうしたもんかと悩んでいたところ、[xsceyさん](https://xscey.github.io/)が解決法を教えて下さいました。（ありがとうございます！）  
　\obeylinesは使わず、以下のようにしてやります。

```LaTeX
\documentclass{utbook}
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
{\catcode`\^^M=\active%
\gdef\xobeylines{\catcode`\^^M\active \def^^M{\par\leavevmode}}%
\global\def^^M{\par\leavevmode}}
\AtBeginDocument{\xobeylines}
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\begin{document}
︙
```

　何やら恐ろしげな呪文ですが、意味は分からなくても大丈夫です。（詳しい技術的な解説は[ブログ](http://hakuoku.hatenablog.com/entry/2016/12/14/222246)の方にあります） こういうTeXへの命令を組み合わせた一種のプログラムを**マクロ**と呼ぶことだけ覚えておいてください。  
　それから%の羅列はただの区切りで、意味はありません。TeXでは頭に半角の`%`をつけた文は本文にも組版にも影響を与えない**コメント**として扱われるので、それを利用してプリアンブル部分を挟んでみました。以降はプリアンブルでの命令はこの区切り線の内側に書いていきます。うるさかったら省いてもOKです。（ただしマクロ行末の％は消さないで！）

　これで、本文通りの改行になりました。

{{< figure src="/img/41linebreak/exobeylines.png" caption="" alt="exobeylines適用後" class="" >}}

　とここまで説明してきましたが、実はこの改行方法は**裏技**です。やってはいけないわけではないんですが、厳密に言えば本来はTeX上級者にのみ許された抜け道と言わねばなりません。  
　どういうことかというと、この改行マクロ（命令の名前は`\xobeylines`です）を使うと、後々紹介するTeXの機能を拡張してくれる種々の命令群（パッケージ）とかち合って予期せぬ結果を引き起こすことがあるんです。  
　このチュートリアルに書かれていることだけをやっている間はいいですが、後々自分でいろいろなパッケージを追加したくなった時に問題が起こる場合があります。煩わしいと思った方は、上記の“正しい”空行方式で改行していくことをおすすめします。詳しくは[改行マクロの副作用](/tutorial/5_7_3xobeylines)の項で取扱いますので、まずはそこまで順番に読んでいってください。

[^1]: [Should the markdown renderer treat a single line break as br? - Meta Stack Exchange](https://meta.stackexchange.com/questions/26011/should-the-markdown-renderer-treat-a-single-line-break-as-br)<br>また[でんでんマークダウン](http://conv.denshochan.com/markdown)では、デフォルトでこの問題をクリアしています。

#### 参考
- [A Beginner’s Book of TEX - Raymond Seroul](https://books.google.com/books/about/A_Beginner_s_Book_of_TEX.html?hl=ja&id=72wKBwAAQBAJ)
　6.4 obeying lines
- [TEX in Practice: Volume III: Tokens, Macros - Stephan v. Bechtolsheim](https://books.google.co.jp/books/about/TEX_in_Practice.html?hl=ja&id=xWvgBwAAQBAJ)
