+++
slug = "accent2"
description = ""
date = "2017-07-20T10:38:56+09:00"
title = "アクセントと特殊記号 後編"
weight = 434
[menu.toc]
    parent = "tateyoko"
+++
&#x3000;コマンドで入力できることは分かったんですが、十蘭のフランス語だのポーの暗号だのをいちいちコマンドで入れてたらイライラしてきます。可読性も下がるし。  
　なので本文には手を加えずに、設定をいじることでアクセント文字や特殊記号も欧文として横倒しさせてしまいましょう。  
（ちなみに青空文庫から取ってきた『ノンシャラン道中記』はアクセント分解という技法を使っていますが、ここでは分かりやすくするためにあらかじめUnicodeのアクセントつきアルファベットに変換してあります）

　具体的にはTeX界のスーパースター・[ZRさん](http://zrbabbler.sp.land.to/)の作成された**px­cjk­cat**パッケージを使います。この人がいなければ日本語TeX組版は今よりもっと悲惨なものになっていただろうというすごいお方です。当サイトでやってることの70％くらいはZRさんのパッケージによっています。

　px­cjk­catは、それぞれの文字が属するグループを変更することのできるパッケージです。今éは日本語の文字と同じグループに入ってしまっているので、英語のグループの方に入れたいと思います。

　プリアンブルでパッケージを読み込んで使います。

```LaTeX
\usepackage[utf8]{inputenc}
\usepackage[<モード>]{pxcjkcat}
```
　`inputenc`パッケージは原稿中にベタ書きするために必要なものです。詳しい説明はこちらを参照してください。  
　[UTF-8 で欧文文字を入力する ～inputenc パッケージ～ - Qiita](https://qiita.com/zr_tex8r/items/b40ca3478e4fe14868e5)

　次の行でpxcjkcatを呼び出しながらモードを指定します。[説明書](http://mirrors.ctan.org/macros/latex/contrib/pxcjkcat/README-ja)によると指定できるモードは4つです。

- forcecjk：upLaTeXのデフォルトと同じ。英語の文字以外は全て全角の和文扱い。
- prefercjk：Adobeの定めるCJK（中日韓）が包括する部分を和文扱いにする。上とさほど変わらない。
- prefercjkvar：上に加え、ギリシャ文字・キリル文字が欧文扱いになる。
- prefernoncjk：漢字・かななど最低限のCJK文字のみを和文扱いにし、それ以外は全て欧文扱い。

　このうち実質的に使うことになるのは後の2つです。どちらを選ぶかは本文の内容によるんですが、まずは一般的と思われる方から見ていきましょう。

#### 横倒ししたい字が少なめな時
　使う外国語が仏独西伊あたりに限られ、éやñや£といった「よくある」字のみを横倒しにしたい場合は`prefercjkvar`を選びます。  
　それだけではほとんどの字が和文扱いになるデフォルトとさして変わらないので、パッケージの機能である`\cjkcategory{<ブロック>,...}{<カテゴリ>}`命令で欧文扱いにしたいグループを追加してやります。

```LaTeX
\usepackage[utf8]{inputenc}
\usepackage[prefercjkvar]{pxcjkcat}
\cjkcategory{latn1}{noncjk}
```

　éや£はUnicodeの「Latin-1 Supplement」というブロックに属しています。なので説明書を検索して、対応する略語である`latn1`を最初のカッコに入れてやります。
　次のカッコではそのブロックを何扱いにするかを指定します。ここでは欧文扱いにしたいので`noncjk`を指定しています。指定できるのは次の5つです。

- noncjk: 欧文扱い
- kanji [または han]: 漢字扱い
- kana: 仮名扱い
- cjk: 「その他の和文」扱い
- hangul: ハングル扱い

　これで見事にアクサンテギュは他のアルファベット同様横向きにできましたが、筆者はこんな副作用が出ました。



　これは×と÷がLatin-1 Supplementに入ってしまっているので欧文扱いになった一方で、全角の＋や＝は全角ゆえにもともと和文扱いになっているためです。  
　別に違和感がなければこのままで大丈夫なんですが、気持ち悪いという時はとりあえず`+-=`を全部半角で打ってしまうという手があります。  
　どうしても×と÷を全角に寄せたい場合、残念ながら同じブロックに入っている記号を別々に指定することはできないので、局所的に手を打つしかありません。`\cjkcategory`や`\cjkcategorymode`を本文中に直接書き込んで、部分的に扱いを変更します。

```LaTeX
\usepackage[utf8]{inputenc}
\usepackage[prefercjkvar]{pxcjkcat}
\cjkcategory{latn1}{noncjk}
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
ここでタヌは、消炭《けしずみ》のかけらを拾って歩道の上へ書きつけた。
\cjkcategory{latn1}{cjk}  %ここでLatin-1を和文扱いにして×と÷を全角に寄せる
400×2＝800 800＋6＝806 806＋40＝846 846＋400＝1246
\cjkcategory{latn1}{noncjk}  %元に戻す
︙
Quand nous étions deux《おまえとふたりでいたときにゃ》 という小唄を口笛で吹きながら、…  %Latin-1が欧文扱いに戻っているのでéが半角横倒しで表示される
```



　十蘭のようにあちこちに出てくるフランス語に比べれば他の記号は大して出てこない、という場合ならこの手が使えると思います。  
　または『黄金虫』のように一箇所だけに半角記号が固まって出てくる場合も局所的な指定でうまくいきます。

```LaTeX
\usepackage[utf8]{inputenc}
\usepackage[prefercjkvar]{pxcjkcat}  %基本的に和文扱い
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
…
髑髏と山羊とのあいだに、赤い色で、次のような記号が乱雑に出ている。――
\cjkcategorymode{prefernoncjk} %ここでモードを切り替え

53‡‡†305))6*;4826)4‡.)4‡);806*;48†8¶60))85;1‡(;:‡*8†83(88)5*†;46(;88*96*?;8)*‡(;485);5*†2:*‡(;4956*2(5*―4)8¶8*;4069285);)6†8)4‡‡;1(‡9;48081;8:8‡1;48†85;4)485†528806*81(‡9;48;(88;4(‡?34;48)4‡;161;:188;‡?;

\cjkcategorymode{prefercjkvar} %元に戻す
「しかし」と私は紙片を彼に返しながら言った。
…
```

（ちなみにこれはこれで一切のスペースがないので、暗号文全体が「ひとつの単語」と認識されてページの外にはみ出してしまいます。その問題は後回しにしてここでは詳述しません）

#### 横倒ししたい字が死ぬほど出てくるとき
　ここまででだいたいのケースには対応できたと思うので、ここからは剛の者の領域です。
　具体的にはLatin-1 Supplementにないőだのāだのいう字が出てくる言語（ハンガリー語やラトビア語）を使いたい人、ソースコードや暗号といった半角記号の列があちこちに出てくるミステリを書いている人など。とにかく欧文扱いする範囲を広くしておきたいので、プリアンブルでモード`prefernoncjk`を指定します。

　ところがこの時本文に♡や☆、●▲■といった、普通横文字の文脈では出て来ない記号が入っているとエラーが出ます。

    Package inputenc Error: Unicode char ♡ (U+2661)
    (inputenc)                not set up for use with LaTeX.

    See the inputenc package documentation for explanation.
    Type  H <return>  for immediate help.
    ...                                              
                                                    
    l.20 ♡

　欧文にない記号まで無理やり欧文扱いしようとしたためこうなります。なので今度は和文扱いしたい記号のブロックを`\cjkcategory`で指定してやります。  
　●▲■のような幾何学的な図形は「Geometric Shapes」、♡や♪のようなその他の記号は「Miscellaneous Symbols」に含まれています。それぞれ略語は`sym18`、`sym19`なのでプリアンブルは次のようになります。

```LaTeX
\usepackage[utf8]{inputenc}
\usepackage[prefernoncjk]{pxcjkcat}
\cjkcategory{sym18,sym19}{cjk}
```

　これでほとんどの場合は大丈夫だと思うんですが、※や二重感嘆符が含まれる「General Punctuation」（`sym04`）など、他のブロックも和文扱いしたいという人もいると思います。その時は前項の内容を参照してUniViewなどで該当ブロックを調べ、[説明書](http://mirrors.ctan.org/macros/latex/contrib/pxcjkcat/README-ja)のページ内検索で略語を見つけて加えていってください。



逆にアクセントつきアルファベットがほんの少ししか出てこない場合は、プリアンブルではなく該当箇所だけで`\cjkcategory{latn1}{noncjk}`を指定すればいいでしょう。（というか正直に言って余計なパッケージ読み込みはせず、[前項](/tutorial/accent1)のコマンドで書いちゃう方が早いです）

{{< figure src="/img/43accent2/prefernoncjk.jpg" caption="" alt="欧文扱い成功" class="" >}}

　できたー！できたよおかあさーん！！これで文中にコマンドを使わずすっきり、かつ望む組版結果になりました。



#### 参考
- [upLaTeX でアクセント付きのラテン文字などがうまく出力されないときの対処法｜Colorless Green Ideas](http://id.fnshr.info/2017/05/27/pxcjkcat/)
- [README-ja](http://mirrors.ctan.org/macros/latex/contrib/pxcjkcat/README-ja)
- [Unicode による文字の入力 [電脳世界の奥底にて]](http://zrbabbler.sp.land.to/unichar.html)
- [［改訂新版］upLaTeXを使おう - Qiita](http://qiita.com/zr_tex8r/items/5c14042078b20edbfb07)
- [UTF-8 で欧文文字を入力する ～inputenc パッケージ～ - Qiita](http://qiita.com/zr_tex8r/items/b40ca3478e4fe14868e5)
- [『その10：upTeXの和文カテゴリコードがアレ』](http://qiita.com/zr_tex8r/items/297154ca924749e62471#%E3%81%9D%E3%81%AE10uptex%E3%81%AE%E5%92%8C%E6%96%87%E3%82%AB%E3%83%86%E3%82%B4%E3%83%AA%E3%82%B3%E3%83%BC%E3%83%89%E3%81%8C%E3%82%A2%E3%83%AC)
