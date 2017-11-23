+++
title = "まとめ"
date = "2017-11-23T00:09:25+09:00"
description = ""
slug = "summary1"
weight = 450
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
\usepackage[prefernoncjk]{pxcjkcat}  %最低限だけCJKであとは全部欧文扱い
\cjkcategory{sym18,sym19}{cjk}  %♡や■を和文扱い　‼やダッシュコマンドを使いたいならsym04を追加

%%%

%改行マクロ
{\catcode`\^^M=\active%
\gdef\xobeylines{\catcode`\^^M\active \def^^M{\par\leavevmode}}%
\global\def^^M{\par\leavevmode}}
\AtBeginDocument{\xobeylines}
%自動インデント禁止
\parindent = 0pt
%連数字の高さを調整
\def\rensuji#1{\hskip\kanjiskip\hbox to 1zw{\yoko\hss\smash{#1}\hss\rule[-0.12zw]{0zw}{1zw}}\hskip\kanjiskip}
%IPAフォントでダブルミニュートを出す
\newcommand{\〟}{\CID{7609}}
%ダッシュの位置調整
\AtBeginDocument{\tbaselineshift = 2.75pt}
%もしくはダッシュコマンドを使う
%\def\――{―\kern-.5zw―\kern-.5zw―}

\makeatletter  %＠が入るマクロはここの内側に書く
%感嘆・疑問符用の連数字コマンド（自動でグルーが入る）
\newcommand{\renmark}[1]{\@ifnextchar」{\rensuji{#1}}{\@ifnextchar』{\rensuji{#1}}{\@ifnextchar）{\rensuji{#1}}{\rensuji{#1}\hspace{1zw}}}}}
%二重記号そのものを使う場合
\def\‼{\@ifnextchar」{‼}{\@ifnextchar』{‼}{\@ifnextchar）{‼}{‼\hspace{1zw}}}}}
\def\⁉{\@ifnextchar」{⁉}{\@ifnextchar』{⁉}{\@ifnextchar）{⁉}{⁉\hspace{1zw}}}}}
\def\⁈{\@ifnextchar」{⁈}{\@ifnextchar』{⁈}{\@ifnextchar）{⁈}{⁈\hspace{1zw}}}}}
\def\⁇{\@ifnextchar」{⁇}{\@ifnextchar』{⁇}{\@ifnextchar）{⁇}{⁇\hspace{1zw}}}}}
\makeatother
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\begin{document}
〝\foreignlanguage{russian}{Братья Карамазовы}\〟の第\rensuji{12}編を読みながらCrème brûléeを食べていた\foreignlanguage{greek}{Ἀριστοτέλης}が唐突に
「――エスト！エスト\renmark{!!}エスト\renmark{!!!}」と叫んだ。
\end{document}
```

　これで基盤編は終了です。次からはよりダイナミックで楽しい、組版らしい組版作業に入っていきます。お疲れ様でした！