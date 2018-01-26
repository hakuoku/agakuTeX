+++
title = "テスト"
date = "2017-01-08T23:02:45+09:00"
lastmod = "2017-01-08"
description = ""
slug = "2_3test"
weight = 230
[menu.toc]
    parent = "setup"
+++

&#x3000;無事にインストールできたかテストしてみます。  
　Windowsのスタートメニューから潜って、「TeXWorks Editor」を起動させます。

{{< figure src="/img/23test/start.png" alt="スタートメニュー" class="" >}}
{{< figure src="/img/23test/works.png" alt="TeXWorks開始画面" class="" >}}

　こんなのが出てきます。これがいわゆるGUIエディタで、TeX文章を読み込ませてPDFを出力させるための窓口になります。  
　とりあえず以下の文をコピーして、白い入力ウインドウに貼り付けます。

```
\documentclass{article}
\begin{document}
Hello World!
\end{document}
```

　「名前をつけて保存」で適当なタイトルをつけて保存し、その後左上の再生ボタン（タイプセットもしくは組版ボタン）を押します。わけの分からん文字列がバーっと出てきても気にせず待ちます。すると、

{{< figure src="/img/23test/pdf.png" alt="最初の組版成功" class="" >}}

　PDFが出てきた！これで成功です！やった！  
　引き続き日本語も読ませてみましょう。以下を試します。

```tex
\documentclass{jsarticle}
\begin{document}
こんにちは，\LaTeX
\end{document}
```

{{< figure src="/img/23test/error.png" alt="エラー" class="" >}}

　PDFが出てきません。ボタンが赤い停止標識になってなにやら不穏な雰囲気。

　実はこれ、[TeXとは](/tutorial/1_2whatstex)の項で書いた「『TeX』という言葉は何を指すのか」に関係があります。TeXというのは慣用的な言葉で、厳密には指しているエンジンは人や国によって違うというくだりです。ボタンの隣を見ると、「pdfLaTeX」になっているかと思います。（あるいはそれ以外でも同じことです）  
　このpdfLaTeXは、アスキーさんのpシリーズとはまた違う、日本語対応していないエンジンになります。だから日本語の文章が読めません。正確には、documentclassで指定しているjsarticleというスタイルが適用できないんです。（jはjapaneseのj）  
　これを読み込ませるためには、日本語のわかるエンジンに切り替えてやるか、あるいは日本語OKなスタイルを捨てる必要があります。

　前者をやってみます。「pdfLaTeX」を押して、下の方の「pLaTeX」に切り替えます。そしてボタンを押して実行。

{{< figure src="/img/23test/konnichiwa_Ink_LI.jpg" caption="" alt="日本語組版成功" class="" >}}

　できた!!　日本語スタイルOKなpLaTeXエンジンのおかげです。  
　後者も試してみましょう。「pdfLaTeX」に戻して、本文のほうをいじります。{jsarticle}のjsを取って{article}にします。

{{< figure src="/img/23test/latex_Ink_LI_Moment.jpg" caption="" alt="部分的に成功" class="" >}}

　LaTeXロゴだけが刷られてきました。これはどうもTeXWorks側の問題らしいんですが、日本語のフォントが全然表示されないんです。できあがったPDFをAdobe Acrobatなんかで表示させると日本語がちゃんと植わっているようですが、いずれにせよ不便なので、今後は日本語を使えるエンジン／スタイルを用いて話を進めます。

　これでテストは完了です。いよいよ本番入ります！

#### 参考
https://texwiki.texjp.org/?LaTeX%20%E3%81%AE%E3%82%A8%E3%83%A9%E3%83%BC%E3%83%A1%E3%83%83%E3%82%BB%E3%83%BC%E3%82%B8#p4b7362a
