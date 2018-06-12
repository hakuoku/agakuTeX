+++
title = "罫囲み（枠をつける）"
date = 2018-03-18T23:34:27+09:00
description = ""
slug = "5_6framed"
weight = 560
topics = ["uline--", "breakfbox", "framed", "varwidth", "minipage", "environ"]
[menu.toc]
    parent = "edit2"
+++

&#x3000;ノンシャラン道中記には名刺や看板の記述など、文が枠で囲まれた箇所がけっこう出てきます。青空文庫では`［＃罫囲み］`となっているところですね。

### インラインでの枠
　文字に枠をつけるにはいろいろなやり方があります。まずは複数行にわたるブロックではなく、行中の一部の文字が囲まれている場合です。これには[傍点・傍線](/tutorial/5_3bouten/)の項で触れた**breakfbox**パッケージを使います。

　ダウンロードの仕方は傍線のところで書いた通りです。なおこのパッケージの使用にはuline--パッケージが必須ですので、傍線を使わない人でも二つのパッケージをどちらも作業フォルダに入れ、プリアンブルで`\usepackage[usetype1]{uline--}`
と`\usepackage{breakfbox}`をどちらも宣言してください。（`pxcjkcat`より**前に**書いてください！）

　これで準備完了です。枠線をつけるには、`\breakfbox{}`で囲みます。

{{< figure src="/img/56framed/fbox.png" caption="" alt="breakfboxによるインラインの枠" class="" >}}

　枠はつきましたが、ちょっと文字との間が空きすぎているような気がしますね。この空きの量は**\fboxsep**というパラメータが決定しています。  
　デフォルトは3ptです。これを0ptに変更してみましょう。

```LaTeX
\fboxsep = 0pt%
　二人が部屋へ入って行くと、\ruby{梁}{はり}の上から丸々と肥った山鳩が三羽飛び下りて来、寝台の下からは、黒い山羊が起きあがって来て、渋い声で\breakfbox{めえ}とないた。
```

{{< figure src="/img/56framed/fboxsep.png" caption="" alt="" class="" >}}

　文字と枠線との間の隙間がなくなり、ぴっちりと描画されるようになりました。これでは狭すぎるようなら、数字をいろいろいじって調整してみてください。  
　同様にして、**\fboxrule**というパラメータで枠の太さを調整できます。デフォルトは0.4ptです。

### ブロックの枠
#### framedパッケージ
　ブロックを枠で囲うにはいくつも方法があります。まずはベーシックな**framed**パッケージを使います。  
　いつものようにプリアンブルでパッケージを呼び出し、framed環境で囲ってやると周りに枠がつきます。

```LaTeX
\usepackage{framed}
%%%%%%%%%%%%%%%%%%%
\leftskip = 3zw%
\begin{framed}%
鉄骨入\ruby{婦人胴着}{コルセ}一手販売

　　　　　　　　　　　アランベエル商会%
\end{framed}%
\leftskip = 0zw%
```

{{< figure src="/img/56framed/framed.png" caption="" alt="framedによる枠" class="" >}}

　ただし、長いブロックだとブロックの途中で次のページや段に行ってしまうことがあります。そんな時framed環境だと、画像のように枠がページや段の境目で閉じてしまい、別々の枠囲みのようになってしまいます。

{{< figure src="/img/56framed/closed.png" caption="" alt="閉じた枠" class="" >}}

　これを開いて連続した枠に変えるにはframedの代わりに**oframed**環境を使ってください。

{{< figure src="/img/56framed/oframed.png" caption="" alt="開いた枠" class="" >}}

### minipage環境
　ところで、「アランベエル商会」の枠囲みですが、ちょっと余白が多いと思いませんか？実はframed環境は、中のテキストの長さに関係なく行の長さいっぱいに枠を描画してしまいます。  
　そうではなく、テキストの長さジャストサイズの枠を引きたい時は、**\fbox**コマンドと**minipage**環境、それに**varwidth**パッケージの合わせ技を使います。

　`minipage`は読んで字のごとく、指定した大きさの小さな「ページ」を作り出す環境です。ページと言ってもいわゆる我々が思う普通のPDFのページではなく、まあただのブロックのようなものです。`\begin{minipage}[位置]{幅}～\end{minipage}`という構文です。  
　`\fbox`というのは前述の`\breakfbox`のように、インラインで枠をつけるコマンドだと思ってください（こっちが元祖で、breakfboxが改良版）。生成したminipageの周りにfboxで線を引くことで、ぴったりの枠囲みが実現できます。

　実際にやってみましょう。枠をつける前はこういう状態です。

```LaTeX
そのうえ、車の背中には、唐草模様の枠の中に、次の様な金文字が麗々しく書かれているのである。
\leftskip = 3zw%
鉄骨入\ruby{婦人胴着}{コルセ}一手販売

　　　　　　　　　　　アランベエル商会
\leftskip = 0zw%
　この華やかな車を一瞥するや否や、あまりの事にコン吉が、
```

{{< figure src="/img/56framed/plain.png" caption="" alt="デフォルトの状態" class="" >}}

　まずこれを、minipage環境で囲ってやります。この時必要になるのがminipageの幅、つまり縦書きにおける長さです。今の場合は「鉄」の字から「会」の字までの距離で、数えてみたら19文字ありました。なので引数に19zwを入れてやります。

```LaTeX
\leftskip = 3zw%
\begin{minipage}{19zw}%
鉄骨入\ruby{婦人胴着}{コルセ}一手販売

　　　　　　　　　　　アランベエル商会%
\end{minipage}
\leftskip = 0zw%
```

{{< figure src="/img/56framed/minipage.png" caption="" alt="minipageに入れた状態" class="" >}}

　少し前後のテキストとの間が詰まっていますね。ルビがめりこんでるし。ですがこれは枠をつけた後で調整しますので、先にfboxで囲んでしまいます。

```LaTeX
\leftskip = 3zw%
\fbox{\begin{minipage}{19zw}%
鉄骨入\ruby{婦人胴着}{コルセ}一手販売

　　　　　　　　　　　アランベエル商会%
\end{minipage}}
\leftskip = 0zw%
```

{{< figure src="/img/56framed/fboxedpage.png" caption="" alt="fboxで枠がついた状態" class="" >}}

　枠がついて、枠線の分前後の空間が空いていい感じに収まりました。  
　今回は上下段の行も揃っていますし、これ以上の調整はなきゃないでよさそうですが、それでもなんとなくまだ前後のテキストとの間が狭い気がします。
　これを調整するには、[前項](/tutorial/5_5fontsize/)の行間の調節で出てきた`\vspace`を使います。今回も余白の幅は行送りの半分にしてみます。

```LaTeX
そのうえ、車の背中には、唐草模様の枠の中に、次の様な金文字が麗々しく書かれているのである。%
\vspace{0.5\baselineskip}
\leftskip = 3zw%
\fbox{\begin{minipage}{19zw}%
鉄骨入\ruby{婦人胴着}{コルセ}一手販売

　　　　　　　　　　　アランベエル商会%
\end{minipage}}%
\vspace{0.5\baselineskip}
\leftskip = 0zw%
　この華やかな車を一瞥するや否や、あまりの事にコン吉が、
```

　`%`と`leftskip`を書く位置が変わっていることに気をつけてください。どうしてかは筆者も分からないんですが、綺麗に入れ子になっていないはずのこの順番で書かないとleftskipが効きませんでした。（改行マクロによって発行される見えない`\par`が効く範囲とか、そういう絡みだと思われる）

{{< figure src="/img/56framed/vspaced.png" caption="" alt="vspaceで調整した状態" class="" >}}

　とにかくこれで余白の調節はできました。なお枠線の外側の余白（いわゆるマージン）ではなく内側の余白（線と中身のテキストの間の距離、いわゆるパディング）を調整するには、前述の`\fboxsep`パラメータを使います。

#### プラスvarwidthパッケージ
　さて、これでジャストサイズの枠が引けるようにはなったんですが、ひとつ問題があります。それはminipageに与えてやる幅のこと。  
　今回は日本語しかない簡単な例だったので、字数を数えるだけでぴったりの数値を割り出すことができましたが、字によってテキストの幅が変わってしまうアルファベットが入るとzwを使うわけにはいきません。そもそも毎回字数を数えるというのがまだるっこしいですしミスの元です。

　これらの問題を解決してくれるのがvarwidthパッケージです。使い方は簡単、プリアンブルで読み込んで、minipage環境の代わりにvarwidth環境を使うだけです。  
　構文は`\begin{varwidth}{幅}～\end{varwidth}`で、必ず幅を渡してやらなければならないことに変わりはないんですが、ここに入れる数値は何でもいいです（正確にはテキストより長い数値なら何でも）。どんな値を入れても、varwidthが枠の幅をテキストに合わせてきちんと縮めてくれます。基本的には行の長さのパラメータである`\linewidth`を入れておけばいいでしょう（テキストがそれ以上に長くなることは基本的にありえないから）。  
　ソースはこうなります。

```LaTeX
\fbox{\begin{varwidth}{\linewidth}%
鉄骨入\ruby{婦人胴着}{コルセ}一手販売

　　　　　　　　　　　アランベエル商会%
\end{varwidth}}%
```

　これで前述の方法と遜色なく、かつ使い回すことのできる枠を作ることができました。ちなみにこれをコンパクトにまとめたものが以下の環境定義になります。`\usepackage{environ}`した上でプリアンブルに入れておけば、該当箇所を`\begin{waku}～\end{waku}`で囲むだけでぴったりの枠が引けます。行末に%をつけるのを忘れないでください。

```LaTeX
\NewEnviron{waku}{\fbox{\begin{varwidth}{\linewidth}\BODY\end{varwidth}}}
```

#### 参考
- [行分割可能な \fbox をつくる - TeX Alchemist Online](http://doratex.hatenablog.jp/entry/20171219/1513609345)
- [QA: 枠囲みと余白について](https://oku.edu.mie-u.ac.jp/tex/mod/forum/discuss.php?d=2393)
- [framed.sty: LaTeX パッケージ](https://www.biwako.shiga-u.ac.jp/sensei/kumazawa/tex/framed.html)
- [天地有情 [LaTeX] framed --- 改ページ可能なフレームの生成](http://konoyonohana.blog.fc2.com/blog-entry-195.html)
- [minipage 環境: LaTeX](https://www.biwako.shiga-u.ac.jp/sensei/kumazawa/tex/minipage.html)
- [varwidth-doc.pdf](http://mirrors.ctan.org/macros/latex/contrib/varwidth/varwidth-doc.pdf)
- [天地有情 [LaTeX] environ --- LaTeX環境用の新しいインターフェース](http://konoyonohana.blog.fc2.com/blog-entry-55.html)