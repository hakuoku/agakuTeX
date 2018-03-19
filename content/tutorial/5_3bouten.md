+++
title = "傍点・傍線"
date = 2018-01-23T00:00:28+09:00
description = ""
slug = "5_3bouten"
weight = 530
topics = ["plext", "pxrubrica", "uline--", "breakfbox", "垂直方向と水平方向"]
[menu.toc]
    parent = "edit2"
+++

&#x3000;ルビが振れるなら傍点だって振れるだろう。はい。振れます。  
　傍点を振る方法は2種類あって、plextパッケージの`\bou`コマンドを使う方法と、pxrubricaパッケージ1.3版の`\kenten`コマンドを使う方法です。

#### \bouコマンド
　使い方は簡単で、単に傍点をつけたい文字を`\bou{}`で囲うだけです。いわゆる普通の黒ゴマ傍点がつきます。

{{< figure src="/img/53bouten/bouten.png" caption="" alt="傍点" class="" >}}

　普段ルビと同じ形式で傍点を振っている人は、前項での一括置換で傍点までルビと同じ`\ruby`形式に変換されてしまったかと思いますので、以下を使ってそれを直してやります。`[・]`（普通の中黒）以外で使っている記号があればそれに変更してください。

　検索する文字列： `\\ruby\{(.+?)\}\{[・]+\}`　→　置換後の文字列： `\\bou{\1}`

#### \kentenコマンド
　こちらも使い方は\bouコマンドと同じで、代わりに`\kenten{}`コマンドを使うだけです。ただしこちらはpxrubrica由来の拡張性に富んでおり、傍点の種類をさまざまに変更することができます。

　傍点記号は縦書き・横書きでそれぞれ主と副、計4種類を設定できるようになっています。今は縦書きなのでそちらの2種類だけ扱うとして、デフォルトは主が黒ゴマ傍点、副が黒丸の圏点です。このうち副記号を使いたい時は、オプションsを指定してやります。

```LaTeX
どうせ、\kenten{まとも}なわれわれがやったって勝てないのに、どうして\kenten[s]{まともでない}公爵の勝つわけがあるものか。
```

{{< figure src="/img/53bouten/subbouten.png" caption="" alt="副傍点を使ったところ" class="" >}}

　デフォルトから記号を変更するには、主が`\kentenmarkintate{マーク}`、副が`\kentensubmarkintate{マーク}`コマンドを使います[^1]。{マーク}のところには、下の表で定義されている記号の名前を書くか、でなければ記号を直に書いちゃうこともできます。後者のやり方ならどんな記号でも指定できるので、トンデモ傍点を振ることも可能です。（ただしもちろんフォントが持っている字形のみ）

|記号|名前|備考|
|:--:|:---|:--|
|・|bullet*|デフォルト|
|•|bullet|※|
|◦|Bullet|※|
|、|sesame*|デフォルト|
|﹅|sesame|※|
|﹆|Sesame|※|
|▲|triangle||
|△|Triangle||
|●|circle||
|○|Circle||
|◎|bullseye||
|◉|fisheye|※|

（※のついた記号を使うにはotfパッケージが必須です）

```LaTeX
\kentenmarkintate{fisheye}
\kentensubmarkintate{☜}
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\kenten{まとも}な、\kenten[s]{まともでない}
```

{{< figure src="/img/53bouten/custom.png" caption="" alt="傍点のカスタマイズ" class="" >}}

　より詳細には、ZRさんによる[解説記事](http://d.hatena.ne.jp/zrbabbler/20170503/1493818510)を参照して下さい。

### 傍線
　もちろん傍線だって引けます。plextパッケージの`\kasen{}`コマンドで囲います。

{{< figure src="/img/53bouten/bousen.png" caption="幸田露伴の「あやしやな」だって組める" alt="傍線" class="" >}}

#### uline--パッケージ
　複雑な傍線には、吉永徹美さんの**uline--**パッケージを使います。TeX Liveには含まれておらず、残念ながらご本人のサイトも2017年に閉鎖されてしまったのですが、[インターネットアーカイブ](https://web.archive.org/web/20161004154816/http://www.h4.dion.ne.jp/~latexcat/)が残っています。また[doraTeX](https://twitter.com/doraTeX)（寺田侑祐）さんが、これを拡張した上でuline--パッケージも同梱した**breakfbox**パッケージを公開していらっしゃいますので、そちらを入手することにしましょう（breakfbox本体も後で使います）。

　[約物](/tutorial/4_4_0punct/)のところで落としたGistと同様、[GitHubのページ](https://github.com/doraTeX/breakfbox)の右上の「Clone or Download」ボタンを押し、「Download ZIP」を選んでダウンロードして下さい。中身のuline--.styとbreakfbox.styを作業フォルダに移し、`\usepackage{uline--}`で宣言して準備完了です。

コマンドは以下。

```LaTeX
\uline{下線} \mline{打消線} \oline{上線}
\udash{下破線} \mdash{打消破線} \odash{上破線}
\uwave{下波線} \mwave{打消波線} \owave{上波線}
\udotline{下点線} \mdotline{打消点線} \odotline{上点線}
```

{{< figure src="/img/53bouten/uline.png" caption="" alt="uline--による各種傍線" class="" >}}

　ここでもタテヨコ反転に気をつけてください。全体が右90°回転しているので、上線が右傍線ということになります（plextは縦書き用パッケージなので`\kasen{}`というコマンドでよかった）。

　デフォルトのままだと波線がややガタついているんですが、これはパッケージ呼び出しの際に`[usetype1]`オプションを入れてやることで治ります。

　二重線にはlinesオプションを使い、`\oline[lines=2]{}`のように書きます。数字のところを変えることで三重以上の傍線も引くことができます。

{{< figure src="/img/53bouten/lines.png" caption="" alt="linesによる多重線" class="" >}}

　その他オプションを指定することで、線の太さや間隔などを変えることができます。詳細はdoraTeXさんの[記事](http://doratex.hatenablog.jp/entry/20171219/1513609345)を参照して下さい。色・太さ・位置の変更で蛍光ペン風の塗り、とかが紹介されています。


[^1]: 横書き時は`\kentenmarkinyoko{マーク}`、`\kentensubmarkinyoko{マーク}`

#### 参考
- [縦書きしてみよう](http://www.fugenji.org/~thomas/texlive-guide/vertical.html)
- [pxrubrica パッケージで圏点できる話 - マクロツイーター](http://d.hatena.ne.jp/zrbabbler/20170503/1493818510)
- [行分割可能な \fbox をつくる - TeX Alchemist Online](http://doratex.hatenablog.jp/entry/20171219/1513609345)
- [TeXが苦手とする処理 - 複数行にわたる下線（あるいは波線・破線など） - TeX Wiki](https://texwiki.texjp.org/?TeX%E3%81%8C%E8%8B%A6%E6%89%8B%E3%81%A8%E3%81%99%E3%82%8B%E5%87%A6%E7%90%86#t65559ac)