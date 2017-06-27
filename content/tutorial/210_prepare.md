+++
title = "準備"
description = ""
date = "2016-12-31T20:04:25+09:00"
lastmod = "2017-01-02"
slug = "prepare"
weight = 210
[menu.toc]
    parent = "setup"
+++

&#x3000;ではさっそく使ってみようじゃないか、と思ったところでまずつまずきます。[ここ](https://texwiki.texjp.org/?TeX%E5%85%A5%E6%89%8B%E6%B3%95)とか[ここ](https://ja.wikibooks.org/wiki/TeX/LaTeX%E5%85%A5%E9%96%80)とか見ても、全然導入方法が分かんない。そもそもインストールって、zipとかexeとかついたファイルをダウンロードして、それをダブルクリックしてちょっとカチカチやれば完了するもんなんじゃないの？  
　と思っていた頃が私にもありました。  
　このへんがTeXの魔道たるゆえんだと思うんですが、そもそも.exeにあたる“TeXの本体”というものがどの辺りを指すのか、私には未だに全く分かりません。  
　いや、正確には発端で書いた通り、e-upTeXのことを指すんでしょうが、これはあくまで組版エンジン単体であって、これだけでは使えないんです。いえ使えますが、素人には魔界の扉みたいに見えるコマンドプロンプトを使わないと動かせないんです。

{{< figure src="/img/21prepare/command.png" caption="魔界の門。呪文が書いてある" alt="CUI" class="">}}

　というわけで、これを呪文を用いずに普通にクリックで操作できるようにするソフトとか、e-upTeXが吐き出したdviファイルなるものをおなじみのPDFに変換するソフトとか、そういうもの全てを含めて組織化した巨大なファイルの集合体が、いわゆる『TeXディストリビューション』というものらしいです。これをまるっとPCに入れてやることで初めて素人も動かせるようになります。そしてそれこそがある意味TeX最大の関門でもあります（インストールが一番辛かったと言う人は多い）。

　[いろんなところ](https://texwiki.texjp.org/?Microsoft%20Windows#distribution)で言われていますが、日本でインストールしたいと思えばディストリビューションはほぼ二択です。

- [TeX Live](https://www.tug.org/texlive/)　国際標準、とにかくどんな言語にもどんな場合にも対応できるようにすさまじい数のファイル群が詰め込まれている。その量なんと4GB超え。
- [W32TeX（TeXインストーラ 3）](http://www.math.sci.hokudai.ac.jp/~abenori/soft/abtexinst.html)　日本人による日本人のための、「誰にでもインストールできるTeX」。TeX Liveよりもスリム。

　導入が簡単なのはTeXインストール3の方で、しかも日本語を扱うために最適な内容となっています。ただし筆者は初っ端からTeX Liveの方に突っ込んでしまいました。多分毒を喰らわば皿まで的な心境だったんでしょう。  
　そこまで多機能じゃなくていい人、ディスクスペースに余裕のない人は[こちら](http://did2memo.net/2016/04/24/easy-latex-install-windows-10-2016-04/)などを参照して、W32TeXのほうで導入してみてください。いろいろやりたい人、多言語フェチ、大きいことはいいことだな人は、TeX Liveにトライしてみましょう。

#### なぜネットワークインストーラを使わないか
　[TeX Wiki](https://texwiki.texjp.org/?TeX%20Live%2FWindows) にはネットワークインストーラの説明が一番に出ていますが、ここでは使いません。代わりにisoイメージによる導入をします。なんでかって？私がネットワークインストールで失敗しまくったからだよ！  
　原因は未だに分かりませんが、こういうエラーが何度も（異なるマシン上でも）出ました。

    TLUtils::check_file: removing /tmp/bd1BBkrSDi/uEpFRVo_Yx/pdfpagediff.doc.tar.xz, sizes differ:
    TLUtils::check_file:   TL=56330, arg=740820
    TLPDB:: install_package: downloading did not succeed
    Installation failed.
    Rerunning the installer will try to restart the installation.
    Or you can restart by running the installer with:
    install-tl --profile installation.profile [EXTRA-ARGS]
    install-tl: Writing log in current directory: /home/daleif/tmp/install-tl-20160523/install-tl.log

　毎回違う名前が入ってたので、多分こっちじゃなく向こうのサーバが悪かったんだと思いたい。  
　この両者は何が違うかと言うと、前述の通りTeX Liveは巨大なファイル群です。ネットワークインストーラはそのファイル群が置いてあるサーバに接続しっぱなしにして、一つずつファイルをダウンロードしながら逐次的にインストールしていく、というもののようです。  
　対してisoイメージは、そのファイル群をあらかじめガッと圧縮したものです。これをブラウザ経由でダウンロードして、しかるのちにオフラインで、マシンの中で解凍するというようになっています。  
　どっちにしろ死ぬほど時間がかかります。isoは筆者の環境では最初のダウンロードに2時間ぐらいかかって、展開は30分くらいでした。ネットワークインストーラはダウンロードとインストールを同時にやるので、それを合計した時間がかかるっぽい。接続状況によっては6時間超えとかもあるらしい。ディスクスペースだけでなく、時間にも余裕のある方のみお試しください。
