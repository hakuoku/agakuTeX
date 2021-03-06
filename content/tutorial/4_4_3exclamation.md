+++
title = "！と？ - 縦中横ふたたび"
date = "2017-11-09T23:13:02+09:00"
description = ""
slug = "4_4_3exclamation"
weight = 443
topics = ["連数字", "plext", "グルー"]
lastmod = "2018-01-27T15:46:49+09:00"
[menu.toc]
    parent = "punctuation"
+++

&#x3000;自動でグルーが入ってしまう感嘆符と疑問符の制御に入るんですが、その前に[縦中横](/tutorial/4_3_1rensuji/#fn:1)のところでちらっと触れた、rensujiの問題を片付けてしまいましょう。上下に小さな空きが入って隣とずれてしまうという問題です。  
　実は`\rensuji{}`コマンドというのはTeX/LaTeXネイティブの命令ではなく、パッケージ**plext**の機能です。日本語の、特に縦書きで活字を並べることをサポートしてくれるパッケージです。ドキュメントクラスにutbookを指定した時点で自動で読み込まれています。  
　このplextを調べてみたところ、どうやら連数字を入れるスペースが全角1文字分の高さより高く設定されているようでした。なのでマクロでrensujiコマンドを設定し直すことにしました。zrjapunct1の中で修正済みです。

```LaTeX
\def\rensuji#1{\hskip\kanjiskip\hbox to 1zw{\yoko\hss\smash{#1}\hss\rule[-0.12zw]{0zw}{1zw}}\hskip\kanjiskip}
```

　例によって意味は分からなくても大丈夫。詳しくは[ブログの記事](http://hakuoku.hatenablog.com/entry/2017/11/23/152241)で説明しています。  
　これで連数字の高さがきちんと他の字と揃いましたので、改めて感嘆符・疑問符についてです。

　普段文章を書く時、！や？の後ろにスペースを入れていますか？筆者は全く入れていません。全角で単独の！の後にも、半角の!?の後にも入れず、次の字とびったりくっつけて書いています。  
　逆に全部に全角スペースを入れているという人もいるでしょう。大事なのは様式を揃えることです。パターンごとに分けて対策を紹介します。

#### 自分でスペースを入れている場合
　基本的にそのままでけっこうです。そうなるとOTFパッケージの自動グルー機能が邪魔なので、オプションで`\usepackage[noreplace]{otf}`と指定してやって無効にします。これで見たまんまで出力されます。  
　ただし全角スペースは一つの独立した“字”とみなされますから、前の行の最後に符号が来て、スペースが行頭に来てしまった時でも他と変わらず出力されます。そこだけ変な字下げが起きてしまうことになります。  
　自分でスペースを入れるという方針上、これを自動で回避する方法はありません。用紙サイズやフォントサイズ、段組みなどが決まった後での校正の段階で、行頭に来てしまったスペースを手で削除していってください。

#### スペースを入れていない場合
　執筆中はスペースを入れないけれど、縦書きである以上組版結果では空きが入っていてほしいですよね。そのためOTFの自動グルー機能に頼ります。これは符号が行末に来た時、次の行頭に空きが入らないように自動で調整してくれます。後の心配をする必要はありません。  
　ただし!?のような半角を2つ並べたものにはグルーが入りません。そこを手で入れてたら本末転倒なので、ある程度自動化してみようと思います。

　`‼`（二重感嘆符記号そのもの）を使っている場合は、zrjapunctパッケージ読み込み時点でこの問題は既に解決しています。普通に書けばOKです。

　二重の符号は全て`\rensuji{}`で入れている時だけ少し注意が必要です。次のような仕組みを仕込んでおいたので、

```LaTeX
\newcommand{\renmark}[1]{%
\@ifnextchar」{\rensuji{#1}}{%
\@ifnextchar』{\rensuji{#1}}{%
\@ifnextchar）{\rensuji{#1}}{%
\@ifnextchar\tczji@J@ellipsis{\rensuji{#1}}{%
\@ifnextchar^^e2{\rensuji{#1}}{\rensuji{#1}\hspace{1zw}}}}}}}
```

　!!・!?・?!・??を囲っているコマンドをrensujiから**`\renmark{}`**に変更します。これで自動でグルーが入るようになりました。一括置換は以下です。  

　　検索する文字列：`\\rensuji\{([!?！？]{2,3})\}`　→　置換する文字列：`\\renmark{\1}`

<br>

<!-- 　`\makeatletter`というのはコマンド名として「＠」を使えるようにするという命令です。`\makeatother`で離脱します。これを書かないで＠入りのマクロを書くとエラーになります。以降もここの内側に書くマクロが出てくるでしょう。   -->

------
（2018/1/27）以下はパッケージができる前のレガシーな内容です

`‼`（二重感嘆符記号そのもの）を使っている場合でもグルーを入れられます。以下のマクロを使います。

```LaTeX
\makeatletter
\def\‼{\@ifnextchar」{‼}{\@ifnextchar』{‼}{\@ifnextchar）{‼}{\@ifnextchar…{‼}{\@ifnextchar―{‼}{‼\hspace{1zw}}}}}}}
\def\⁉{\@ifnextchar」{⁉}{\@ifnextchar』{⁉}{\@ifnextchar）{⁉}{\@ifnextchar…{⁉}{\@ifnextchar―{⁉}{⁉\hspace{1zw}}}}}}}
\def\⁈{\@ifnextchar」{⁈}{\@ifnextchar』{⁈}{\@ifnextchar）{⁈}{\@ifnextchar…{⁈}{\@ifnextchar―{⁈}{⁈\hspace{1zw}}}}}}}
\def\⁇{\@ifnextchar」{⁇}{\@ifnextchar』{⁇}{\@ifnextchar）{⁇}{\@ifnextchar…{⁇}{\@ifnextchar―{⁇}{⁇\hspace{1zw}}}}}}}
\makeatother
```

　本文に書く時には、ただの‼ではなく`\‼`と入れてください。これで記号自体が一種のコマンドのようになって自動で空きを入れてくれます。

　~~そしてすいません、このページのやりかただと、受け側のカギ括弧!!」の直前にはグルーが入らないようになっていますが、カギ括弧以外の丸括弧!!　）やその他括弧!!　｝の前にはグルーが入ってしまいます。二重感嘆符は会話で使われるのが最も多いだろうと考えてのことですがやはり片手落ちです。今の筆者の技術力ではこれが精一杯でした……いい方法がありましたらご教授ください。~~

（2017/11/17追記）  
　ZRさんが解決策を教えて下さいました！上のコードも修正してあります。  
　`\renmark`・`\‼`ともに、`\@ifnextchar`の後に入っている閉じカッコを変えれば対応カッコの種類を変えることができます。ネスト（入れ子構造）を追加すれば3種類以上にも増やせます。

（2017/12/01追記）  
　感嘆符類の後に続く句読点やリーダー類のことを考えていなかったのでさらに修正しました。


#### 参考
- [LaTeXによる小説誌制作のヒント ｜ 文藝部LaTeX研究会](https://qdaibungei.github.io/latex/2017/10/12/book-making-hints.html)
- [Understanding \@ifnextchar - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/57788/understanding-ifnextchar)
- [How to peek and test whether the next character is a digit? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/323311/how-to-peek-and-test-whether-the-next-character-is-a-digit)
