+++
title = "note：変数と長さの単位"
date = "2017-11-19T10:08:20+09:00"
description = ""
slug = "4_4_7parameter"
weight = 447
lastmod = "2017-11-20T14:43:11+09:00"
topics = ["zw", "パラメータ（変数）", "代入"]
[menu.toc]
    parent = "punctuation"
+++

&#x3000;ちょこっとだけプログラミングっぽい話します。先ほど出てきた`\tbaselineshift`や字下げの項で使った`\parindent`、バックスラッシュがついていますがこれらはコマンド（制御命令）ではなく**変数**［**パラメータ**］です。

　変数はプログラミングの基盤となる重要な概念ですが難しいことはありません。すごく簡単に言うと「設定値」のことです。よく使われるメタファーとしては、「中に数値を自由に出し入れできる、ラベルが貼られた箱」という言い方があります。`\ホニャララ`というのはそのラベルです。  
　parindentを例に取ると、TeXは段落の頭に差しかかった時にこの箱の中を覗いて収められている数値を参照します。デフォルトでは1zw（全角1文字分）という数字が入っているので、TeXはその通りに1文字下げてから改めて段落本文を見て、そこにある全角スペースも文字として普通に組んじゃうので結果2字下げになってしまうんでした。  
　なのでプリアンブルで`\parindent = 0pt`と1から0に書き換えてやることで、行頭におけるTeXの振る舞いを「0字下げ」に変え、望む動作にすることができました。  
　この書き換えを正確には「**代入**」といいます。_ｘ_ や _y_ に数字を代入するように、parindentに0を代入しているんです。イコールは代入記号で、「等しい」という意味ではないので注意してください。

　コマンドが`\どうこう[こんなふうに]{ナントカ}`のように「ナントカをこんなふうにどうこうする」という形を取るのに対して、変数は上記のような特性があるので、基本的に`\ラベル = 数値`という形で値をセットすることになります。「操作」と「設定」の違いがあるよ、というだけの話です。覚えておくと混乱が少なくなるかもしれません。

　そういった数値につく「単位」の意味を今まで説明していなかったので、ここに挙げておきます。

|単位|意味|
|:-:|:--|
|cm|センチメートル|
|mm|ミリメートル|
|in|インチ（1in = 2.54cm）|
|pt|ポイント（72.27pt = 1in）|
|bp|ビッグポイント（72bp = 1in）|
|sp|スケールドポイント（65336sp = 1pt）|
|em|現在の欧文フォントの“M”の字の幅|
|ex|“x”の字の高さ|
|zw|現在の和文フォントの文字幅|

　わけわかんないですね。特にインチが体感的にどれぐらいか分かっていない日本人にはポイントのあたりがキツいです。なので把握できる単位だけ使う方針で全然OKです。  
　多分zwを一番多用することになるでしょう。zenkaku widthの略で、文字通り全角文字の正方形のボックスの幅のことです。（正方形なのでzw = zhです。お作法としてzhは使わないほうがいいことになっています）  
　字詰めやベースラインのバランスなど、フォントに依存する要素はzwやem、ページ設定のように普通に定規で測れる要素はcmやmmを使うといいと思います。