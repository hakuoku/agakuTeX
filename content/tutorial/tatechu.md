+++
topics = ["連数字", "アクセント分解"]
description = ""
title = "全角と半角・縦中横・記号の制御"
slug = "tatechu"
date = "2017-05-07T08:54:46+09:00"
lastmod = "2017-06-26T18:36:43+09:00"
[menu.toc]
    parent = "edit"
+++
&#x3000;十蘭の小説にはフランス語が山ほど出てきます。青空文庫ではデフォルトで、横倒しにして欧文として表示したい箇所は半角、横倒しにせずカナと同じように縦向きで表示したいアルファベットは全角で書かれています。  
　TeXでもこれは全く同じです。なので縦向きで組みたい英数字は全角にしておきます。

{{< figure src="/img/44/zenkaku.jpg" caption="" alt="全角で縦向き" class="" >}}

　ただし全角フォントが気に入らなかったり表示がおかしくなったりする場合があります。それから2つ以上の英数を1字分のスペースに押し込んで縦向きにしたい時もよくあります。青空文庫なら`39［＃「39」は縦中横］`となっている部分です。  
　そんな時は**rensuji**コマンドを使います。半角文字を半角のまま、いわば「全角一文字分の高さのスペースにおける横書き」にしてくれます。  
　実際に見た方が早いです。<code class="language-latex">一様に&#092;rensuji{39}度の一夜を</code>のように書いてやるとこうなります。

{{< figure src="/img/44/rensuji.jpg" caption="" alt="連数字" class="" >}}

　めんどくさいのが !! や !? の扱いです。全角で書くと縦に二つ、半角で書くと横倒しで二つ表示されてしまうので、二重・三重の感嘆符は

　欧文は基本的に半角で書いておけばいいんですが、ここに英語以外の外国語使いにとっての罠があります。本文中に普通にé（アキュートアクセントつきe。よく出る）と書くと、結果はこういうことになります。

{{< figure src="/img/44/" caption="悪夢" alt="eだけが縦書きになった仏文" class="" >}}

　例え半角幅のアルファベットでも、upLaTeXのデフォルトでは“英語に含まれていない字”はカナや漢字と同じ全角文字のくくりに入るので、和文のように縦に組まれてしまうんです。  
　なので対策を打ちます。特殊な字の出現頻度や普段の執筆スタイルによって方法が変わります。

#### 多言語ライトユーザー向け（伝統的な方法）
　そんなに英語以外の外国語を使わない人、自前のキーボードから外国文字を入力できなくて毎回コピペで取って来てる人、そもそも最初から直書きをせずにアクセント分解を使っている人はこの方法を取ります。エスケープの時と同様、コマンドで記号を入れるやり方です。  
　[アクセント記号: LaTeX](http://www.biwako.shiga-u.ac.jp/sensei/kumazawa/tex/accent.html)のページや、[チートシート](https://wtsnjp.com/pdf/platexsheet.pdf)1ページ目の「アクセント類」のところを見て文中にコマンドを入力してください。  
　`\アクセントコマンド（つけたい文字）`のようになっており、例は主にaにつけるようになっていますが、もちろん他のアルファベット（大文字含む）にも使えます。
　`\d a`のように、コマンドとつけたい字が半角スペースで離れているものは`\d{a}`のような波括弧で囲ったものと同義です。好みで使い分けてください。

　[標準的なアクセント分解](http://cosmoshouse.com/tools/acc-conv-j.htm)イコール青空文庫の形式を使っている場合は置換ができます。


#### 多言語ヘビーユーザー向け（進化した方法）
　十蘭並みに外国語を使う人、キーボードカスタマイズばっちりしてて直書きができる人（スマホから入力含む）、もう外国文字がいっぱい入ったファイルがあって今更変換したくない人はこっちです。設定をいじることで、特殊文字を和文（全角）ではない欧文として認識させます。




<!--　半角英数はそのまま半角で書けば横向きになりますが、悩ましいのが本文との間のスペースです。
　青空文庫では`のごとき Renault の Les Stella、`のように、和文との間に半角スペースを入れ、句読点との間では省いています。筆者自身は和文や他の記号との間には一切スペースを入れません。これはもう個人の執筆スタイルの問題なので統一しようとするのは無理がある気がします。
　スペースを入れるか入れないかでどう結果が変わるかはドキュメントクラスによりますが、utbookでは-->

#### 参考
- [縦書きしてみよう](http://www.fugenji.org/~thomas/texlive-guide/vertical.html)
- [私家版日本語 LaTeX テンプレート（2017年5月版）｜Colorless Green Ideas](http://id.fnshr.info/2017/05/20/my-latex-templates-201705/#toc12)
- [upLaTeXを使おう [電脳世界の奥底にて]](http://zrbabbler.sp.land.to/uplatex.html)