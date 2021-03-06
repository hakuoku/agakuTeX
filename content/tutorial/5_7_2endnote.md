+++
title = "後注"
date = 2018-04-04T11:06:51+09:00
description = ""
slug = "5_7_2endnote"
weight = 572
topics = ["endnote", "etoolbox", "disobeylines","xobeylines"]
lastmod = "2018-04-30T22:04:51+09:00"
[menu.toc]
    parent = "footnote"
+++

### 後注（尾注）

　小説だといちいちページごとに脚注を入れるのではなく、話が終わった後でまとめて注を出したい、と思う場合が多いでしょう。その場合は**endnotes**パッケージを使います。  
　ちょっと注意が必要なのが導入の仕方。パッケージ宣言と共に以下の2行目を入れるのを忘れないでください。

```LaTeX
\usepackage{endnotes}
\let\footnote=\endnote
```

　これであとは普通に`\footnote{}`で注をつけ、章末や巻末など注記を出したいところに**`\theendnotes`**コマンドを書けば後注が出力されます。1章ごとに1番から始めたい場合は、`\theendnotes`の後に`\setcounter{endnote}{0}%`を書き込んでください。

　と、ここで終わりたいところなんですがいくつか問題が。endnotesパッケージはこれまでカスタマイズしてきた脚注記号のスタイルを無にした上、縦書きにそぐわない体裁にしてくれやがります。

{{< figure src="/img/57endnote/endnotes.jpg" caption="" alt="横倒しになった脚注記号" class="" >}}

　奥歯をギリギリと噛み締めつつ設定のし直しです。まずはパッケージ宣言を`\usepackage{endnotes,etoolbox}`として、endnotesの**後に**etoolboxが読み込まれるようにします。パッケージはこんなふうに繋げて複数を読み込むこともできます。  
　そして以下をプリアンブルにペースト。

```LaTeX
\renewcommand{\makeenmark}{\raisebox{1zw}{\makebox[0zw]{\scriptsize\hspace{1zw}\rensuji{$\theenmark$}}}}% \raiseboxで横の距離を、\scriptsizeで文字サイズを、\hspaceで縦の距離を調整
\patchcmd{\theendnotes}
  {\makeatletter}
  {\makeatletter\renewcommand\makeenmark{\hbox{\rensuji{$\theenmark$} }}}
  {}{}
```

　あとは`\renewcommand{\theendnote}{(\arabic{endnote})}`の形で、前項の表の8つのコマンドおよびカッコを入れるなどの微調整が行えます。（ただし筆者の環境では`\fnsymbol`が使えませんでした……原因は調査中です）

#### 体裁の変更
{{< figure src="/img/57endnote/ruby.png" caption="" alt="ルビと親文字が逆転している" class="" >}}

　後注本体の体裁はこんな感じ……なんですが、明らかに問題がありますね。そうです、ルビの表示がおかしいんです。  
　これも例によって改行マクロの副作用です。あと注同士の間が妙に空いているのもそのせいです。  
　というわけで、一旦改行マクロであるxobeylinesを無効にしてやるという手を使います。改行マクロの下に、以下のような記述を加えてください。

```LaTeX
\def\disobeylines{\catcode `\^^M=5 }
```

　'dis'obeylinesという名の通り、obeylinesの作用をリセットする命令です。そして`\theendnotes`を`\disobeylines`と`\xobeylines`で挟みます。

```LaTeX
\disobeylines
\theendnotes
\xobeylines
```

{{< figure src="/img/57endnote/rubykai.png" caption="" alt="正常なルビ" class="" >}}

　これでルビが意図通りの表示になりました。  
　しかし今度はちょっと行間がつまり過ぎな気がしますね。実は文字サイズが本文より小さいのでそう見えています。なので体裁を変更していきましょう。

　タイトルである「Notes」を変更するには`\renewcommand{\notesname}{Notes}`を使います。第二引数を好きな文字列に書き換えてください。空白にすればタイトルを出さないこともできます。  
　タイトルは今太字でLargeの大きさ、注本文はfootnotesizeの大きさになっています。これらを変更するには`\makeatletter`の内側で次のようにしてください。  
　厳密にはタイトルは文書構造のところでやる`\section`によって定義されているので、そこを直接いじったほうがいい場合もありますが、ここでは応急処置として後注のタイトルのスタイルのみ変えてしまいます。

```LaTeX
\renewcommand\enoteheading{\section*{\mdseries\Large\notesname% タイトルを太字にしたくない時に\mdseriesを指定、次で文字サイズを指定
  \@mkboth{\MakeUppercase{\notesname}}{\MakeUppercase{\notesname}}}% 上の柱にタイトルを表示したくなければ\MakeUppercase{\notesname}を消す
  \mbox{}\par\vskip-\baselineskip}% \vskipでタイトルと注本体の間を調整
\renewcommand\enoteformat{\rightskip\z@ \leftskip\z@ \parindent=1.8em% \parindentでインデント量を指定
  \leavevmode\llap{\makeenmark}}
\renewcommand\enotesize{\normalsize}% ここで注本体の文字サイズを指定
```

　正直この方法で正しいのか筆者も分かってないんですが……とりあえず体裁は変更できるということで。こんな感じです。

{{< figure src="/img/57endnote/changed.png" caption="" alt="体裁を変更した後注" class="" >}}

#### 参考
- [LaTeXで脚注を文書末もしくは章末に書く手順 - 503 Service Unavailable](http://hnsn1202.hateblo.jp/entry/2013/02/06/170617)
- [LaTeX tiny Tips](http://koichi.nihon.to/psnl/latex0.html)
- [古典籍の為のＴｅＸ](http://www.orcaland.gr.jp/~utsunomiya/TeX.htm#%82R%81j%8C%E3%92%8D%83}%83N%83%8D%82%C9%82%C2%82%A2%82%C4)
- [formatting - Endnotes do not be superscript and add a space - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/99984/endnotes-do-not-be-superscript-and-add-a-space)
- [plain tex - Is there a counterpart/antidote for \obeylines? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/57318/is-there-a-counterpart-antidote-for-obeylines)