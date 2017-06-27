+++
date = "2017-04-19T21:37:32+09:00"
lastmond = "2017-04-22T14:36:27+09:00"
description = ""
title = "ドキュメントクラスの設定"
slug = "documentclass"
weight = 340
[menu.toc]
    parent = "generate"
+++
&#x3000;組めたはいいけど横書きだし余白めっちゃあるし何なん？って感じですね。これは一番最初の文である`\documentclass{article}`に問題があります。  
　この文は「どの**ドキュメントクラス**を使うか」ということを宣言しています。今はarticleです。ドキュメントクラスとは拡張子.clsのファイルのことで、デザイン情報が書かれたスタイルシートのようなものです（TeX Liveインストールフォルダの奥深くに存在している）。文書をどんな設定、どんなレイアウト、どんなデザインにするかは全てこれが握っています。全く同一の本文でも、クラスを取り替えることでガラッと違うレイアウトにできたりします。

　「article」は超基本的な、英語の記事や小論のためのクラスです。テストで使ったjsarticleはTeX界の巨人・[奥村先生](https://oku.edu.mie-u.ac.jp/~okumura/)の作った、日本語横書き版articleクラスです。文章の規模が増えると「report」、「book」というように使うクラスも大きくしていきます。  
　他にもTeX Liveには山のようなクラスが収録されていて、中には編み物の編み図を描くためのknittingクラスとか、正方形のCDジャケットを作れるcdcoverクラスとかぶっ飛んだものもあります。誰がいつ使うんだろう。  
　「じゃあ縦書きでA5とか新書版とかな小説用のクラスを使えばいいんだね！」となります。然り。ただし実は日本語を書くためのクラスは多くなく、限られた選択肢から選んだ上で細かいところは自分の手で設定していかなければなりません。  
　中でも縦書き用のクラスはt系列に限られます。Unicode用にはutarticle、utreport、utbookが用意されており、小説を組みたいとなれば選択肢は**utbook**一択です。  
（PDFオンリーの電子書籍にしたい人はutreportを選びましょう。左右でレイアウトが変わらない、つまり製本の時のノドを考慮しないのがreportクラスになります）

　そんな状況の中、2017年2月に衝撃的な出来事がありました。あべのりさんこと[阿部紀行氏](http://www.math.sci.hokudai.ac.jp/~abenori/)の開発した、**[jlreqクラス](https://github.com/abenori/jlreq)**がリリースされたんです。  
　「JLReq」とは、ウェブの親玉W3C（Web技術の標準化団体）が発表した「[日本語組版処理の要件](https://www.w3.org/TR/jlreq/ja/)」のことで、JIS X 4051「日本語文書の組版方法」を元に策定されており、ざっくり言えば前者はWeb、後者は紙で日本語を組む時に用いられる公式規格ということです。  
　それをTeX上で実現しようということで作られたのがjlreq.clsで、これがほんとに綺麗に日本語を組めます。日本語のみならずCJK（中日韓）界隈に革命が起きたのではというくらい素晴らしいクラスなんですが、いかんせんこれを書いている17年4月の段階でまだまだ出来たてで、細部が詰まっていないところがあるようです。これからどんどん仕様が変わっていくでしょう。

　というわけで本項では安定版として、utbookを使った方法で組版していきます。将来的にはjlreqクラスを使う方法に揃えたいですが、現段階ではNightly Buildとして別項で紹介します。  
　なので、一行目を<code class=" language-latex">\documentclass{utbook}</code>に変更します。これで組んでみましょう。

{{< figure src="/img/34documentclass/tate.png" caption="" alt="utbook適用後" class="" >}}

　縦書きできた!!　嬉しい！　自分の文章がちゃんとした形になって出て来るのはいつになっても楽しいです。  
　次項でさらに小説本文にふさわしい組み方にします。

#### 参考
- [にっき♪](http://abenori.blogspot.com/2017/02/jlreq_9.html)
- [クラスファイル一覧 - TeX Wiki](https://texwiki.texjp.org/?%E3%82%AF%E3%83%A9%E3%82%B9%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E4%B8%80%E8%A6%A7)
- [The TeX Catalogue OnLine, Topic Index](http://texcatalogue.ctan.org/bytopic.html#cd)