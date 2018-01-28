+++
title = "まとめ"
date = "2017-11-23T00:09:25+09:00"
description = ""
slug = "4_5summary1"
weight = 450
lastmod = "2018-01-27T15:46:18+09:00"
[menu.toc]
    parent = "edit"
+++

&#x3000;ここまでのまとめとして、現時点でのソースの様子を載せておきます。  
　この例はパッケージや自動処理を最大限使った場合のものになっているので、皆さんのそれぞれの原稿とはオプションなどが異なっていると思います。自分の文体に合った構成にして、エラーが出るようなら各ページをもう一度確認してみてください。

```LaTeX
\documentclass[uplatex]{utbook}  %OTFや以降のパッケージのためにuplatexオプションを入れておく
%%%%%%%%%%%%%%%%
%パッケージ使用はここでまとめて宣言
\usepackage{otf}  %pxcjkcatより前に書くこと　！と？の後の自動グルーを許可しない場合はnoreplaceオプションを入れる
\usepackage[LGR,T2A,T1]{fontenc}  %前2つがギリシャ・キリル文字のために必要
\usepackage[greek,russian,english,japanese]{babel}  %同上
\usepackage{textcomp}
\usepackage[utf8]{inputenc}
\usepackage[prefercjkvar]{pxcjkcat}  %英語・ギリシャ・キリル以外は全部和文扱い
\cjkcategory{latn1,latnA}{noncjk}  %Latin-1 SupplementとExtended-Aを欧文扱い
\usepackage{zrjapunct1}  %.styファイルを同フォルダに入れた上で宣言　pxcjkcatより後に書くこと

%%%

%改行マクロ
{\catcode`\^^M=\active%
\gdef\xobeylines{\catcode`\^^M\active \def^^M{\par\leavevmode}}%
\global\def^^M{\par\leavevmode}}
\AtBeginDocument{\xobeylines}
%自動インデント禁止
\parindent = 0pt
%IPAフォントでダブルミニュートを出す　もしくは‶ダブルプライム″を使うこと
\newcommand{\〟}{\CID{7609}}
%欧文ダッシュ（ベースライン）の位置調整
\AtBeginDocument{\tbaselineshift = 2.75pt}
%%%%%%%%%%%%%%%%%%%
\begin{document}
〝\foreignlanguage{russian}{Братья Карамазовы}\〟の第\rensuji{12}編を読みながらCrème brûléeを食べていた\foreignlanguage{greek}{Ἀριστοτέλης}が唐突に
「------エスト！エスト\renmark{!!}エスト\renmark{!!!}」と叫んだ。
\end{document}
```

{{< figure src="/img/45summary1/summary.png" caption="" alt="まとめの組版結果" class="" >}}

　これで基盤編は終了です。次からはよりダイナミックで楽しい、組版らしい組版作業に入っていきます。お疲れ様でした！