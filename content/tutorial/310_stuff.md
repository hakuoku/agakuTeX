+++
title = "いるもの"
description = ""
date = "2017-04-02T14:41:40+09:00"
lastmod = "2017-04-18T17:58:20+09:00"
slug = "stuff"
weight = 310
topics = ["青空文庫形式"]
[menu.toc]
    parent = "generate"
+++
&#x3000;満を持して本番の組版に入りたいところですが、まずは必要なものを用意します。

- テキスト

　組版したい文章がないと始まらない。この入門では[青空文庫](http://www.aozora.gr.jp/)からお借りします。  
　青空文庫は著作権の切れた作家の作品の一大アーカイブサイトです。見たことない人はこれを期にアクセスしてみてね。乱歩も太宰も宮沢賢治もあるよ。  
　そしてまた、日本語の小説を本の通りに表記することにかけては今のところデファクトスタンダードのプロジェクトと言っていいと思います（2017年現在）。そもそもが「既存の本をデジタルデータにして永続的に保存する」という目的のサイトなので、そのための方法が蓄積されています。

　青空文庫ではTeXと同じように、小説本文に特殊な指示を書き込むことで表示を実現しています。`青空《あおぞら》`でルビとか、`（上）事実［＃「（上）事実」は大見出し］`とか。今だとpixivでも青空形式からの変換が使えますよね。（詳しい文法は[注記一覧](http://www.aozora.gr.jp/annotation/)を参照）  
　このように全て日本語で非常に直感的な文法なので、筆者はベタ書きの時はこの記法を使っていました。今も一部使っています。ただPDF等他の形式への変換はなかなか難しいものがあったのでTeXに切り替えたという側面もあります。  
　そんなわけでここからの解説も、青空文庫のルールに一部沿う形で進めていきます。もちろん青空記法に従わず素のテキストから作ることもできますよ。

　すでにワープロで書き上げた原稿をお持ちの方は、あらかじめプレーンテキストに変換してやってください。Wordなら保存する時に「テキストファイル」を選ぶとできます。他のサービスやアプリを使っている人はエクスポート機能を使うか（拡張子は必ず.txtで）、本文をPCのメモ帳にコピペして保存しておきましょう。

　さて、そんな青空文庫の中で個人的に最もしんどい部類に入ると思われる作家、[久生十蘭](http://www.aozora.gr.jp/index_pages/person1224.html)をピックアップ。一番好きな「ノンシャラン道中記」シリーズを選びました。短編連作だから章立ての練習もできるし。  
　どうしんどいかはまあこれを見てくれ。

{{< figure src="/img/31stuff/juran.png" caption="" alt="久生十蘭サンプル" class="" >}}

　どうですこのルビの乱舞。漢字モノルビ、漢字グループルビ、フランス語にカタカナルビ、日本語の文にまるごとフランス語ルビと鬼のような混み入り具合です。もちろんアクサンテギュバリバリ。ハングインデントとか看板っぽいレイアウトとかも出てくる。挿絵もある。死ぬ。盛りだくさんで素材としてはぴったりです。

　ごちゃごちゃ具合にびびりつつ、まずは青空文庫の作品ページからzipを落としてきます。展開して中の.txtファイルを開いてみると、中はこんな感じです。

{{< figure src="/img/31stuff/aozora.png" caption="" alt="青空文庫テキストサンプル" class="" >}}

　青や緑の字がエンジンに伝える特殊な指示です。TeXもこんな風に、本文に注記をガリガリ書き込むことで組版していきます。  
<br>

- テキストエディタ

　テキストエディタというのはプレーンテキストを編集するためのソフトで、原理は「メモ帳」と一緒です。付加情報がない質素なやつ。ただし情報を持ってないのはあくまで“文書そのもの”なので、編集する時にはソフト側のフィルター次第で本文と注記を分けたり見やすくできたりします。テストや上の画像で字に色がついて見えたのもこれのおかげです。TeXに限らず、自分に合ったエディタをひとつ持っておくと何かと便利です。  
　テストで使ったTeXWorksはTeX専用の統合開発環境ですが、テキストエディタであるとも言えます。どのエディタで書いても結局最後はTeXWorksに通すので、初めからこれで書くのもいいと思います。（ただし使い勝手はあまりよくない）  
　既に好みのものがあるなら勿論そちらを使ってください。基本的に既存の.txtファイルにコマンドを書き込んでいくだけなので、わざわざTeXのために執筆環境を変える必要はありません。

　ちなみに筆者は「[Mery](http://www.haijin-boys.com/wiki/%E3%83%A1%E3%82%A4%E3%83%B3%E3%83%9A%E3%83%BC%E3%82%B8)」というエディタを溺愛しています。純国産、シンプルでキュートで軽快でとにかくひたすら使いやすい！色分け以外にも置換やマクロなどの強力な機能があり、細かい動作までカスタマイズできます。作者のkuro様に[感謝](http://www.haijin-boys.com/11.html)です。  
　最近ではGitHub製の「[Atom](https://atom.io/)」がクールだとの評判で、使っている人も多いです。いちいち長いコマンドを打ち込まずに済む自動補完機能などを備えた、プログラミング用の高機能で先進的なエディタです。ただし便利な分複雑で、ヘルプも全て英語なので体力のある人が挑戦するといいでしょう。  
　ここではMeryを使って解説します。どれがいいのかわからない時はとりあえずMeryにしときましょう。組版結果を見るためのスクリーンショットにはTeXWorksと標準のPDFプレビューが登場します。

#### あると便利なもの
- 高校程度の英語力もしくはサッと引ける辞書

　これから行うのは日本語の組版ですが、TeXに与える指示は全て英語をベースとしたコマンドです。そしてTeX本体が返してくるメッセージや警告も全て英語です。プログラミングでエラーが出た時は「検索するより先に辞書を引け」というのが初心者の鉄則です。まずエラー文が何を言ってるか訳して理解すればそれで解決しちゃう時もあるし、理解してから検索した方が効率もいいからです。  
　あとは大概のエラーや疑問は[TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/)のようなQ&Aサイトで出尽くしてるんですが、これがオール英語です。辞書やGoogle翻訳を味方につければ、日本語訳されていない問題にぶち当たっても自力でザクザク先に進めます。

- PDF編集ソフト

　テストで出てきたように、TeXWorksには組み込みのPDFビューワーがついていますし、完成したPDF原稿を後で見るにもお馴染みのAdobe Acrobat Readerを使えばいいので、新しいソフトを入れないといけないわけではありません。ただ組版の後半の方になってくると、正直TeXを介さず直接PDFをいじった方が早い工程とかが出てきます。そんな場合に備えて、閲覧だけでなく編集もできる軽快なソフトがあると便利でしょう。  
　本家本元の[Adobe Acrobat DC](https://acrobat.adobe.com/jp/ja/acrobat.html)が使えたらいいんでしょうが、有償の上動作もあまり軽くないです。[窓の杜](http://forest.watch.impress.co.jp/library/nav/genre/offc/document_pdf.html)などから好みのソフトを探してみてください。

#### 参考
- [PDFの作り方 - TeX Wiki](https://texwiki.texjp.org/?PDF%E3%81%AE%E4%BD%9C%E3%82%8A%E6%96%B9)
- [PDF - TeX Wiki](https://texwiki.texjp.org/?PDF)