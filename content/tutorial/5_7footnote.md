+++
title = "脚注・尾注"
date = 2018-03-26T12:07:18+09:00
description = ""
slug = "5_7footnote"
weight = 570
eyecatch = "/img/57footnote/footnote.png"
topics = ["footnote"]
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


　ところがですね、

#### 参考
- [LaTeXコマンド集 - 脚注](http://www.latex-cmd.com/struct/footnote.html)
- [LaTeXコマンド - 脚注の番号・ラベルを変更](https://medemanabu.net/latex/footnote-label/)
- [QA: 和文文字と脚注番号の間のアキ](https://oku.edu.mie-u.ac.jp/tex/mod/forum/discuss.php?d=1783)
- [Change the color of footnote marker in LaTeX - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/26693/change-the-color-of-footnote-marker-in-latex?rq=1)