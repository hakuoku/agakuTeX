+++
title = "インストール"
description = ""
date = "2017-01-03T14:25:46+09:00"
lastmod = "2017-01-08"
slug = "install"
weight = 22
[menu.toc]
    parent = "setup"

+++

&#x3000;いよいよインストールにかかります。  
　まず念のためウイルスチェックソフトを切っておきます。起きてると障害になることがあるらしいので。たいていは一番下のタスクバーの通知領域にセキュリティソフトのアイコンが入ってるので、お使いのソフトのメニューに沿って機能を一旦オフにしてください。  
　[Acquiring TeX Live as an ISO image ](http://www.tug.org/texlive/acquire-iso.html)のページにアクセスして、・download from a nearby CTAN mirrorというリンクをクリックします。たくさんサーバがある中で、自動的に一番近いところまで飛ばしてくれます。筆者はこんな画面が出ました。

{{< figure src="/img/22install/ctan.png" caption="" alt="ctan" class="center" >}}

<<<<<<< Updated upstream
　どこのページに飛んでも、その中のtexlive2016.isoをクリックします。ポップアップが出るので、「ファイルに保存する」を選びます。

{{< figure src="/img/22install/download_Ink_LI.jpg" caption="" alt="download" class="center" >}}
=======
{{< figure src="/img/22install/ctan.png" alt="最寄りのctan" class="" >}}

　どこのページに飛んでも、その中の**texlive2016.iso**をクリックします。ポップアップが出るので、「ファイルに保存する」を選びます。

{{< figure src="/img/22install/download_Ink_LI.jpg" alt="ダウンロード／ファイルに保存" class="" >}}
>>>>>>> Stashed changes

　地獄の長時間ダウンロードが始まります。図にあるように2.9GBありました。2時間ほどPCを放っておいて散歩にでも行きましょう。

　｜帰宅｜　λ...........

　ダウンロードが完了したら、ブラウザによって表示は違いますが、ダウンロードメニューから「保存フォルダを開く」で保存先に飛んでください。そこからisoイメージを、一応Cドライブ直下に移しておきます（切り取り＆貼り付け、もしくはドラッグ＆ドロップでOK）。  
　Windows8以降の場合、標準でisoを取り扱えますので、右クリックして「マウント」を選びます。DVDドライブとして展開されるかと思います。

<<<<<<< Updated upstream
{{< figure src="/img/22install/isomini.png" caption="↓" alt="mount iso" class="center" >}}
{{< figure src="/img/22install/mountedmini.png" caption="" alt="mounted" class="center" >}}
=======
{{< figure src="/img/22install/isomini.png" caption="↓" alt="isoを仮想ドライブとしてマウント" class="" >}}
{{< figure src="/img/22install/mountedmini.png" caption="" alt="マウント結果" class="" >}}
>>>>>>> Stashed changes

　Windows7以前の場合は、isoを直接マウントできないので、ソフトを追加してからの展開になります。まず[Virtual CloneDrive ](http://forest.watch.impress.co.jp/library/software/vclonedrive/)などの専用ソフトをインストールし、そのソフトの操作法に従ってマウントします。

　無事にマウントされたらひとまずそれは置いておいて、次に10も8も7も追加ソフトが要ります。perlが入ってない環境だと、この時点ではまだGUIインストーラが動かないはずです。  
　[ActiveState](http://www.activestate.com/activeperl)からActivePerlを取ってきます。サイトの中の「Community Edition」、念のためx86版をクリックしてダウンロードします。これは普通のインストールで、アイコンをダブルクリックして画面に従ってカチカチやるだけです。

　青いperlの六角形が入ったら、マウントしたDVDドライブに戻って中のinstall-tl-windows.batをダブルクリックします。

<<<<<<< Updated upstream
{{< figure src="/img/22install/perl_Ink.jpg" caption="" alt="perl installed" class="center" >}}

　魔界の門ことコマンドプロンプトが出てきますが大丈夫。しばらくすると、こんなウィンドウが出てきます。

{{< figure src="/img/22install/live.png" caption="" alt="TeX Live wizard" class="center" >}}
=======
{{< figure src="/img/22install/perl.png" alt="batをダブルクリック" class="" >}}

　魔界の門ことコマンドプロンプトが出てきますが大丈夫。しばらくすると、こんなウィンドウが出てきます。

{{< figure src="/img/22install/live.png" alt="TeX Live wizard" class="" >}}
>>>>>>> Stashed changes

　あとは画面の指示に従って、じゃかじゃか「次へ」をクリック。最後に「導入」を押せば、isoイメージからの展開／インストールが始まります。30分かそれ以上かかります。  
　この画面出てこねーよ！という時は、ひとまず気長に待ってみてください。かなり重い工程のようなので……  
　最終的に、「TeX Liveへようこそ！」という文があればインストール完了です。お疲れ様でした！

<<<<<<< Updated upstream
{{< figure src="/img/22install/welcome.png" caption="" alt="welcome" class="center" >}}
=======
{{< figure src="/img/22install/welcome.png" alt="TeX Liveへようこそ！" class="" >}}
>>>>>>> Stashed changes

