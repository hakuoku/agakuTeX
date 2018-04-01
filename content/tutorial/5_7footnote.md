+++
title = "脚注・後注"
date = 2018-03-26T12:07:18+09:00
description = ""
slug = "5_7footnote"
weight = 570
eyecatch = "/img/57footnote/kaburi.png"
topics = ["footnote", "rule", "hspace", "endnote", "etoolbox","makeatletter","makeatother"]
[menu.toc]
    parent = "edit2"
+++

&#x3000;註のつけ方です。まずは一番シンプルな、**`\footnote`**コマンドを使ってみます。  
　注をつけたい箇所に、`\footnote`で囲んで脚注の文章を入れます。

```LaTeX
いささが\footnote{「いささが」は原文ママ}空腹の模様でもある、
```

　するとこんなふうに、

{{< figure src="/img/57footnote/footnote.png" caption="" alt="ページ末尾に脚注" class="" >}}

　本文には脚注番号がつき、ページの最後に脚注が表示されます。

　脚注記号のスタイルを変更するには、以下のコマンドをプリアンブルに書き込んでやります。`\renewcommand`というのもマクロ命令で、読んで字の如く既存の命令を新しく書き換えるコマンドになります。この場合は`\thefootnote`という既に規定されている（どこでかは知らん）記号の定義を第二引数の中身で書き換えています。

|コマンド|スタイル|
|:-------|:------:|
|`\renewcommand{\thefootnote}{\arabic{footnote}}`|1 2 3 …|
|`\renewcommand{\thefootnote}{*\arabic{footnote}}`|*1 *2 *3 …|
|`\renewcommand{\thefootnote}{\arabic{footnote})}`|1) 2) 3) …|
|`\renewcommand{\thefootnote}{\alph{footnote}}`|a b c …|
|`\renewcommand{\thefootnote}{\Alph{footnote}}`|A B C …|
|`\renewcommand{\thefootnote}{\roman{footnote}}`|ⅰ ⅱ ⅲ …|
|`\renewcommand{\thefootnote}{\Roman{footnote}}`|Ⅰ Ⅱ Ⅲ…|
|`\renewcommand{\thefootnote}{\fnsymbol{footnote}}`|*†‡§¶…|

　`{*\arabic{footnote}}`や`{\arabic{footnote})}`を見れば分かるように、第二引数はある程度自由に変更できます。`{(\roman{footnote})}`とすれば(ⅰ) (ⅱ) (ⅲ)…のような記号を振れたり。

### 脚注記号の調整
　ところがですね、ルビの振ってある箇所に脚注をつけようとすると、以下のように記号とルビがかぶってしまいます。

{{< figure src="/img/57footnote/kaburi.png" caption="ちきしょう" alt="ルビと脚注記号が重なる" class="" >}}

　これを直すには上の、脚注記号を変更するというテクニックに頼ります。  
　使うのは**`\rule`**コマンド。これは真っ黒い長方形を描画することのできるコマンドです。`\rule[深さ]{幅}{高さ}`の形で使います。  
　深さって何？と思われるでしょうが、これは英語ならではの概念です。[カッコ類](/tutorial/4_4_5brackets)のところでやったベースラインから、gやyの字の先端が達する一番の下端までの距離のことです。  
　深さを把握できると箱を自由自在に操れるようになる（らしい）んですが、今は特に使わないので、とりあえずそういうオプションがあるということだけ知っておいてください。筆者も未だに苦手です。

　この長方形はいろいろな使いでがありますが、ここでは幅をゼロにして「見えない支柱」にして`\thefootnote`の定義に入れてやるという使い方をします。

　そもそも脚注記号`\thefootnote`は、こんな感じの箱として領域が確保されています。

{{< figure src="/img/57footnote/box.png" caption="" alt="脚注記号を囲む箱" class="" >}}

　だだかぶりですね。なのでこの枠の中に高いruleの支柱を立て強制的に枠自体を大きくし、それによって「2」がもっと下の方に描画されるようにしたいと思います。

　具体的にやってみましょう。まずは幅を持たせたまま、ruleを描画してみます。

```LaTeX
\renewcommand{\thefootnote}{\rule{10pt}{10pt}\arabic{footnote}}
```

{{< figure src="/img/57footnote/rule.png" caption="" alt="2の前に1zw×1zwの黒い箱" class="" >}}

　2の前に10pt×10ptの黒い箱が描かれました。これでruleのイメージはなんとなく掴んで頂けたかと思います。  
（ちなみに本当はzwを使いたいんですが諦めました。相対的な単位だと、後でやる作業と干渉しあって思わぬ副作用が出る場合があります）  
　そこでruleの幅をゼロにして見えなくします。（ついでに便宜上つけていた枠も取っ払います。実際はxcolorというパッケージを使っていました）

```LaTeX
\renewcommand{\thefootnote}{\rule{0pt}{10pt}\arabic{footnote}}
```

{{< figure src="/img/57footnote/rule0.png" caption="" alt="" class="" >}}

　ちょっと遠いですかね。あとは結果を見ながら微調整していくしかなさそうです。ここでは最終的に8ptの高さにしました。

　さてこうなると今度は、ルビと比べて少しボディテキストから横に離れすぎてるような気がしてきました。  
　これはさっきのような`\thefootnote`への追記では直せません。仕方がないので力技に頼ります。こんな記述をつかいます。

```LaTeX
    \def\@makefnmark{\hbox{\ifydir $\m@th^{\@thefnmark}$
      \else\hbox{\yoko$\m@th^{\@thefnmark}$}\fi}}%
```

　この恐ろしげな呪文は我々が使っているutbookクラスのファイルから持ってきたものです。脚注記号はこの部分が規定しているので、これを少しいじって文書ファイル側にペーストすることで上書きしてやる、ということになります。  
　以降もこういう、クラスファイルの断片をコピペするというアレなやり方がけっこう出てきます。本当はクラス自体をカスタマイズできればいいんでしょうが、それはかなり高度な領域の話になるのでここではあくまでちまちましたやり方で通します。

　上の記述をこんなふうに改変して、プリアンブルに入れてやります。

```LaTeX
\makeatletter
\renewcommand\@makefnmark{\hbox{\ifydir $\m@th^{\@thefnmark}$
    \else\hbox{\yoko$\hspace{-1pt}\m@th^{\@thefnmark}$}\fi}}% \hspace{-1pt}が入った
\makeatother
```

　普通のTeX文書中では`@`を含んだコマンド名は使えません。なので`\makeatletter`と`\makeatother`で挟んでやる必要があります。以降もアットマークが出てきたら、基本的に`\makeatletter`の中に入れるんだと思ってください。  
　内側が本題になります。`\hspace{}`とは、文字サイズや罫囲みのところで使った`\vspace{}`の水平方向＝文字送り方向版です。カッコの中に入れた数値の分だけスペースを入れてくれます。  
　縦書きの中においてはタテヨコ反転するんだがらhorizontal spaceは下方向へのそれじゃないのか、と思うかもしれませんが、今は直前の`\yoko`という命令が一時的に組方向を横にしています。なので、ruleが脚注記号の上ではなく前に入ったように、脚注の箱の中は横書きです。

　マイナス数値を入れることで横方向に箱を詰め、数字とボディテキストを近づけることができました。

{{< figure src="/img/57footnote/hspace.png" caption="" alt="横の距離を調節" class="" >}}

　以上のテクニックを組み合わせるといろんな脚注記号のカスタマイズができます。例えば縦書き書籍でよく見るこういう![縦書きのカッコと数字](/img/57footnote/tate.png)記号にしたい時は、プリアンブルに以下を入れることで可能になります。本文のフォントやフォントサイズを変えると齟齬が出てくると思いますので、その時はコメントにある数値を変えることで微調整してください。

```LaTeX
\renewcommand\thefootnote{\scriptsize(\rensuji{\arabic{footnote}})}% \scriptsizeで大きさを調整
\renewcommand\@makefnmark{\hbox{\ifydir $\m@th^{\@thefnmark}$
    \else\lower 2.5pt \hbox{\hspace{2pt}$\m@th^{\@thefnmark}$}\fi}}% \lower 2.5ptで横の距離を、\hspace{2pt}で縦の距離を調整
\long\def\@makefntext#1{\parindent 1zw\noindent
    \raise 1.5pt \hb@xt@ 2zw{\hss\@makefnmark}#1}% \raise 1.5ptで脚注本体の方の記号のズレを修正
```

### 後注（尾注）

　小説だといちいちページごとに脚注を入れるのではなく、話が終わった後でまとめて注を出したい、と思うことが大半でしょう。その場合は**endnotes**パッケージを使います。  
　ちょっと注意が必要なのが導入の仕方。パッケージ宣言と共に以下の2行目を入れるのを忘れないでください。

```LaTeX
\usepackage{endnotes}
\let\footnote=\endnote
```

　これであとは普通に`\footnote{}`で注をつけ、章末や巻末など注記を出したいところに**`\theendnotes`**コマンドを書けば後注が出力されるんですが、ここで一つ問題が。endnotesパッケージはこれまでカスタマイズしてきた脚注記号などのスタイルを無にした上、縦書きにそぐわない体裁にしてくれやがります。

{{< figure src="/img/57footnote/endnotes.jpg" caption="" alt="横倒しになった脚注記号" class="" >}}

　奥歯をギリギリと噛み締めつつ設定のし直しです。まずはパッケージ宣言を`\usepackage{endnotes,etoolbox}`として、endnotesの**後に**etoolboxが読み込まれるようにします。パッケージはこんなふうに繋げて複数を読み込むこともできます。  
　そして以下をプリアンブルにペースト。

```LaTeX
\renewcommand\makeenmark{\raisebox{0.8zw}{\makebox[0zw]{\hspace{1zw}\rensuji{\@textsuperscript{\normalfont\@theenmark}}}}}% \raiseboxで横の距離を、\hspaceで縦の距離を調整
\patchcmd{\theendnotes}
  {\makeatletter}
  {\makeatletter\renewcommand\makeenmark{\hbox{\rensuji{\@textsuperscript{\normalfont\@theenmark}}}}}
  {}{}
```

　あとは`\renewcommand{\theendnote}{(\arabic{endnote})}`の形で、上の表の8つのコマンドおよびカッコを入れるなどの微調整が行えます。（ただし筆者の環境では`\fnsymbol`が使えませんでした……原因は調査中です）

#### 体裁の変更
　後注の体裁は上の画像のようになります。  
　タイトルである「Notes」を変更するには`\renewcommand{\notesname}{註}`を使います。第二引数を好きな文字列に書き換えてください。空白にすればタイトルを出さないこともできます。

　タイトルは今太字でLargeの大きさ、注本文はfootnotesizeの大きさになっています。これを変更するには次のようにしてください。  
　厳密にはタイトルは文書構造のところでやる`\section`によって定義されているので、そこを直接いじったほうがいい場合もありますが、ここでは応急処置として後注のタイトルのスタイルのみ変えてしまいます。

```LaTeX
\renewcommand\enoteheading{\section*{\mdseries\normalsize\notesname% タイトルを太字にしたくない時に\mdseriesを指定、次で文字サイズを指定
  \@mkboth{\MakeUppercase{\notesname}}{\MakeUppercase{\notesname}}}%
  \mbox{}\par\vskip-\baselineskip}
\renewcommand\enotesize{\normalsize}% ここで注本体の文字サイズを指定
\renewcommand\enoteformat{\rightskip\z@ \leftskip\z@ \parindent=1.8em \parskip = -1zw% \parskipで行間を調整
```

　正直この方法で正しいのか筆者も全然分かってないんですが……とりあえず体裁は変更できます。こんな感じです。

{{< figure src="/img/57footnote/tweaked.png" caption="" alt="体裁を変更した後注" class="" >}}

#### 参考
- [LaTeXコマンド集 - 脚注](http://www.latex-cmd.com/struct/footnote.html)
- [LaTeXコマンド - 脚注の番号・ラベルを変更](https://medemanabu.net/latex/footnote-label/)
- [QA: 和文文字と脚注番号の間のアキ](https://oku.edu.mie-u.ac.jp/tex/mod/forum/discuss.php?d=1783)
- [Change the color of footnote marker in LaTeX - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/26693/change-the-color-of-footnote-marker-in-latex?rq=1)
- [LaTeXで脚注を文書末もしくは章末に書く手順 - 503 Service Unavailable](http://hnsn1202.hateblo.jp/entry/2013/02/06/170617)
- [LaTeX tiny Tips](http://koichi.nihon.to/psnl/latex0.html)
- [古典籍の為のＴｅＸ](http://www.orcaland.gr.jp/~utsunomiya/TeX.htm#%82R%81j%8C%E3%92%8D%83}%83N%83%8D%82%C9%82%C2%82%A2%82%C4)
- [formatting - Endnotes do not be superscript and add a space - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/99984/endnotes-do-not-be-superscript-and-add-a-space)
- [LaTeX/Boxes - Wikibooks, open books for an open world](https://en.wikibooks.org/wiki/LaTeX/Boxes)