+++
date = "2017-06-28T20:18:41+09:00"
title = "アクセントと特殊記号 (1)"
weight = 433
slug = "accent1"
description = ""
topics = ["パッケージ"]
[menu.toc]
    parent = "tateyoko"
+++
&#x3000;縦向きにしたい英数字の処理はできました。横倒しにしたい欧文は普通に半角で書いておけばいいんですが、ここに英語以外の外国語使いにとっての罠があります。本文中にé（アキュートアクセントつきe。よく出る）などが含まれていると、結果はこういうことになります。

{{< figure src="/img/43accent1/accent.jpg" caption="悪夢" alt="eだけが縦書きになった仏文" class="" >}}

　例え半角幅のアルファベットでも、upLaTeXのデフォルトでは“英語に含まれていない字”はカナや漢字と同じ全角文字のくくりに入るので、和文のように縦に組まれてしまうんです。  
　フランス語とか使わないし、という人でも要注意です。£や†といった、一見普通の半角っぽい記号でも同じ現象が起こります。記号がミソの暗号ミステリ、『黄金虫』なんかでやってみるとひどいことになります。  

{{< figure src="/img/43accent1/GoldBug.jpg" caption="縦横ごっちゃ" alt="記号の一部だけが縦組みになっている" class="" >}}

　こうしてはいられないので対策を取るんですが、その前に重要な機能である「**パッケージ**」について説明してしまいます。記号の表示が全然問題ない人もここだけは覚えていってください。

　**パッケージ**とは要するにTeXの拡張機能のことで、素のままのTeXにはできない様々な機能を提供してくれるものです。ブラウザのアドオンなんかに似てますね。  
　これの実体はTeXへの命令が書かれた.styファイルで、ドキュメントクラスと同様膨大な数がTeX Liveの奥深くに収録されています。まだ収録されていない最新のものをサイトからダウンロードして使うこともできます。TeX文書のプリアンブルで、必要なものを呼び出すことによって使用できるようになります。  

　実際にやってみましょう。プリアンブルの、今まで書いたマクロなどの前の行に以下を入れます。

```LaTeX
\usepackage[T1]{fontenc}
\usepackage{textcomp}
```

　`\usepackage[オプション]{パッケージ名}`という形になります。1行目はfontencパッケージによりT1エンコーディングを選択、２行目はtextcompパッケージを読み込んでいます。  
　この二つのパッケージの機能や意味は分からなくてもOKです。とりあえずおまじない＆パッケージ呼び出しの基礎として書いておいてください。

　さてこれを踏まえた上で、縦向きになってしまう字の対策をします。

#### 古典的な方法
　そんなに英語以外の外国語や記号を使わない人、自前のキーボードから特殊記号を入力できなくて毎回コピペで取って来てる人、そもそも最初から直書きをせずにアクセント分解を使っている人はこの方法を取ります。エスケープの時と同様、コマンドで記号を入れるやり方です。

　以下の表を見て文中にコマンドを書き込んでください。[アクセント記号: LaTeX](http://www.biwako.shiga-u.ac.jp/sensei/kumazawa/tex/accent.html)のページや、[チートシート](https://wtsnjp.com/pdf/platexsheet.pdf)1ページ目も参照。

<table>
    <tbody>
        <tr><td>¡</td><td><code>!`</code></td><td>¿</td><td><code>?`</code><td>à</td><td><code>\`a</code></td>
<td>á</td><td><code>\'a</code></td></td></tr>
        <tr><td>ã</td><td><code>\~a</code></td><td>â</td><td><code>\^a</code></td><td>ä</td><td><code>\"a</code></td><td>ā</td><td><code>\=a</code></td></tr>
        <tr><td>ė</td><td><code>\.{e}</code></td><td>ç</td><td><code>\c{c}</code></td><td>å</td><td><code>\r{a}</code></td><td>ă</td><td><code>\u{a}</code></td></tr>
        <tr><td>ě</td><td><code>\v{e}</code></td><td>ő</td><td><code>\H{o}</code></td><td>oȏ</td><td><code>\t{oo}</code></td><td>ẹ</td><td><code>\d{e}</code></td></tr>
        <tr><td>ṉ</td><td><code>\b{n}</code></td><td>ß</td><td><code>{\ss}</code></td><td>æ</td><td><code>{\ae}</code></td><td>Æ</td><td><code>{\AE}</code></td></tr>
        <tr><td>œ</td><td><code>{\oe}</code></td><td>Œ</td><td><code>{\OE}</code></td><td>ø</td><td><code>{\o}</code></td><td>Ø</td><td><code>{\O}</code></td></tr>
        <tr><td>ł</td><td><code>{\l}</code></td><td>Ł</td><td><code>{\L}</code></td><td>ı</td><td><code>{\i}</code></td><td>ȷ</td><td><code>{\j}</code></td></tr>
    </tbody>
</table>

　`\アクセントコマンド{つけたい文字}`のようになっており、組み合わせを変えればどんな字にでもアクセントがつけられます。かなや漢字でもOK。

<!-- 　[標準的なアクセント分解](http://cosmoshouse.com/tools/acc-conv-j.htm)イコール青空文庫の形式を使っている場合は置換ができます。 -->

　記号はこちら。

<table>
    <tbody>
        <tr>
            <td>&amp;</td><td><code>\&amp;</code></td>
            <td>†</td><td><code>\dag</code></td>
            <td>~</td><td><code>\textasciitilde</code></td>
            <td>\</td><td><code>\textbackslash</code></td>
        </tr>
        <tr>
            <td>%</td><td><code>\%</code></td>
            <td>‡</td><td><code>\ddag</code></td>
            <td>~</td><td><code>\textasciicircum</code></td>
            <td>|</td><td><code>\textbar</code></td>
        </tr>
        <tr>
            <td>#</td><td><code>\#</code></td>
            <td>…</td><td><code>\dots</code></td>
            <td>™</td><td><code>\texttrademark</code></td>
            <td>‖</td><td><code>\textbardbl</code></td>
        </tr>
        <tr>
            <td>_</td><td><code>\_</code></td>
            <td>©</td><td><code>\copyright</code></td>
            <td>®</td><td><code>\textregistered</code></td>
            <td>•</td><td><code>\textbullet</code></td>
        </tr>
        <tr>
            <td>$</td><td><code>\$</code></td>
            <td>£</td><td><code>\pounds</code></td>
            <td>ª</td><td><code>\textordfeminine</code></td>
            <td><</td><td><code>\textless</code></td>
        </tr>
        <tr>
            <td>¶</td><td><code>\P</code></td>
            <td>§</td><td><code>\S</code></td>
            <td>º</td><td><code>\textordmasculine</code></td>
            <td>></td><td><code>\textgreater</code></td>
        </tr>
    </tbody>
</table>

　大体エスケープのところでやったのとかぶってますね。まあほぼほぼ「縦向きでいい記号は全角直打ち、横向きにしたい記号はコマンドで入れる」と覚えておけば適切に使い分けられると思います。こんな感じです。
```LaTeX
チャゲ＆飛鳥　%これは全角のアンド
DEAN \& DELUCA　%こっちは半角のアンド（コマンド）

インテル® 入ってる？　%直接書いた登録商標マーク
intel{\textregistered} inside.　%コマンドの登録商標マーク
```

{{< figure src="/img/43accent1/marks.png" caption="" alt="同じ記号の組方向による使い分け" class="" >}}

　ちなみに上の表のコマンド群はTeXのネイティブ命令なんですが、冒頭でtextcompパッケージを読み込んでいるので、その拡張コマンドを使って入れられる記号の種類が増えています。[textcomp.sty: LaTeX パッケージ](http://www.biwako.shiga-u.ac.jp/sensei/kumazawa/tex/textcomp.html) のページに使える記号とコマンドが載っていますので、必要な人は見てみてください。かわいい葉っぱのマークやなんかがあります。
