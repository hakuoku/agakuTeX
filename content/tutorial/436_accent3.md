+++
title = "アクセントと特殊記号 (3)"
date = "2017-10-10T11:15:56+09:00"
description = ""
slug = "accent3"
weight = "436"
topics = ["ギリシャ・キリル文字", "フォントエンコーディング", "Babel"]
[menu.toc]
    parent = "tateyoko"
+++

&#x3000;さて話を戻して、pxcjkcatパッケージの使い方の続きです。

#### 横倒ししたい字が死ぬほど出てくるとき
　いちいち部分指定なんかしてられない！というぐらい半角にしたい文字が多い時には、プリアンブルで呼び出す時に`prefernoncjk`モードを指定します。最低限のCJK文字だけ和文扱いであとは全部欧文扱いにしてくれるモードです。

　ところがこの時本文に♡や☆、●▲■といった、普通横文字の文脈では出てこない記号が入っているとエラーが出ます。

    Package inputenc Error: Unicode char ♡ (U+2661)
    (inputenc)                not set up for use with LaTeX.

    See the inputenc package documentation for explanation.
    Type  H <return>  for immediate help.
    ...                                              
                                                    
    l.20 ♡

　欧文にない記号まで無理やり欧文扱いしようとしたためこうなります。なので今度は和文扱いしたい記号のブロックを`\cjkcategory`で指定してやります。  
　●▲■のような幾何学的な図形は「Geometric Shapes」、♡や♪のようなその他の記号は「Miscellaneous Symbols」に含まれています。それぞれブロックIDは`sym18`、`sym19`なのでプリアンブルは次のようになります。

```LaTeX
\usepackage[utf8]{inputenc}
\usepackage[prefernoncjk]{pxcjkcat}
\cjkcategory{sym18,sym19}{cjk}
```

　これでほとんどの場合は大丈夫だと思うんですが、人によってはまだエラーが出るでしょう。またエラーは出ないけど※や二重感嘆符が含まれる「General Punctuation」（`sym04`）など、他のブロックも和文扱いしたいという人もいると思います。その時は[前項](/tutorial/Unicode/)に従ってUniViewで該当ブロックを調べ、pxcjkcatの説明書＝[README](http://mirrors.ctan.org/macros/latex/contrib/pxcjkcat/README-ja)をページ内検索して対応するブロックIDを加えていってください。

#### ラスボス
　そしてここまでやってもなお横書きできないのがギリシャ文字とキリル文字です。和文扱いだと縦になるし欧文扱いだとエラーになります(´・ω・`)

{{< figure src="/img/43accent3/pgrtate.jpg" caption="なんか変" alt="縦組みになったキリル文字" class="" >}}
{{< figure src="/img/43accent3/pgr.jpg" caption="" alt="エラーになったキリル文字" class="" >}}

　結論だけ先に申しますと、以下のように書けば横倒しできます。どうしても文中にコマンドが必要になります。

```LaTeX
\usepackage[LGR,T2A,T1]{fontenc}  %一番最初に書いたおまじないをこのように変える
\usepackage{textcomp}
\usepackage[utf8]{inputenc}
\usepackage[prefernoncjk]{pxcjkcat}
\cjkcategory{sym18,sym19}{cjk}
\usepackage[greek,russian,english,japanese]{babel}  %使用言語をオプションで列挙し、最後はメインの日本語にする
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
カラマーゾフの兄弟（原題：\foreignlanguage{russian}{Братья Карамазовы}）において、

「\foreignlanguage{greek}{Μοιρα}」というアルバムを

m9(\textasciicircum\foreignlanguage{russian}{Д}\textasciicircum)
```

{{< figure src="/img/43accent3/babel.jpg" caption="" alt="横倒し成功" class="" >}}

　か、かっこ悪い……特に最後、エスケープと合わさって何書いてあるかわかんねえよ。  
　しかしこれ以外にやりようがありません。`\foreignlanguage{<言語>}{<内容>}`コマンドの第2引数にはその言語の文字のみ入れられて、普通のアルファベットや日本語と混在させてはいけないんです。  
　このコマンドは上で呼び出している**Babel**パッケージによって使えるようになった命令です。バベルという名の通り、文書を多言語対応にしてくれる強力なパッケージなんですが、強力ゆえに何がどこまでできるのか筆者がまだ理解できてません。とりあえずこう使えば言語を切り替えられるらしいよ、とだけ言っておきますorz

　ここの挙動について詳しくは[ブログ](http://hakuoku.hatenablog.com/entry/2017/10/10/231839)で説明していますので、仕組みを知りたいかたは読んでみてください。特にフォントエンコーディングという重要かつややこしい概念が出てくるので、今は読まなくても頭の片隅に置いておくといざという時役に立つかもしれません。

　なおヨーロッパ語以外の言語、例えばアラビア語などは筆者の範疇を超えてしまいます。申し訳ありませんがご自身で調べてください。

#### 参考
- [upLaTeX でアクセント付きのラテン文字などがうまく出力されないときの対処法｜Colorless Green Ideas](http://id.fnshr.info/2017/05/27/pxcjkcat/)
- pxcjkctの[README-ja](http://mirrors.ctan.org/macros/latex/contrib/pxcjkcat/README-ja)
- [Unicode による文字の入力 [電脳世界の奥底にて]](http://zrbabbler.sp.land.to/unichar.html)
- [［改訂新版］upLaTeXを使おう - Qiita](http://qiita.com/zr_tex8r/items/5c14042078b20edbfb07)
- [UTF-8 で欧文文字を入力する ～inputenc パッケージ～ - Qiita](http://qiita.com/zr_tex8r/items/b40ca3478e4fe14868e5)
- [『その10：upTeXの和文カテゴリコードがアレ』](http://qiita.com/zr_tex8r/items/297154ca924749e62471#%E3%81%9D%E3%81%AE10uptex%E3%81%AE%E5%92%8C%E6%96%87%E3%82%AB%E3%83%86%E3%82%B4%E3%83%AA%E3%82%B3%E3%83%BC%E3%83%89%E3%81%8C%E3%82%A2%E3%83%AC)
- [pTeXと多言語処理 - TeX Wiki](https://texwiki.texjp.org/?cmd=read&page=pTeX%E3%81%A8%E5%A4%9A%E8%A8%80%E8%AA%9E%E5%87%A6%E7%90%86&word=%E3%82%AD%E3%83%AA%E3%83%AB%E6%96%87%E5%AD%97)