+++
slug = "accent2"
description = ""
date = "2017-07-20T10:38:56+09:00"
title = "アクセントと特殊記号 後編"
weight = 434
[menu.toc]
    parent = "tateyoko"
+++
&#x3000;コマンドで入力できることは分かったんですが、十蘭のフランス語だのポーの暗号だのをいちいちコマンドで入れてたらイライラしてきます。置換ができるとはいえ可読性下がるし。  
　なので本文には手を加えずに、設定をいじることでアクセント文字や特殊記号も欧文として横倒しさせてしまいましょう。

　具体的にはTeX界のスーパースター・[ZRさん](http://zrbabbler.sp.land.to/)の作成された**px­cjk­cat**パッケージを使います。この人がいなければ日本語TeX組版は今よりもっと悲惨なものになっていただろうというすごいお方です。当サイトでやってることの70％くらいはZRさんのパッケージによっています。

　pxcjkcatと、関係するパッケージをプリアンブルで読み込みます。

```LaTeX
\usepackage{bxbase}
\usepackage[bxutf8]{inputenc}
\usepackage[prefernoncjk]{pxcjkcat}
```

　BXbaseはZRさんのBX・PXシリーズの基盤になるパッケージです。これを読み込むことで、次のinputencで普通のutf8ではない、ZR版のbxutf8が指定できるようになります。  
（正直この辺は正確なことはさっぱり分かんないまま書いてます。特にinputencの意味と挙動が謎すぎる。ここに至るまでの試行錯誤と詳しい解説らしきものはブログの方にありますので、不明な点があったら見てみてください）

　これで本題のpxcjkcatが使えるようになりました。これはそれぞれの文字が属するグループを変更することのできるパッケージです。今éは日本語の文字と同じグループに入っちゃってるので、英語のグループの方に入れたいわけです。  
　[説明書](http://mirrors.ctan.org/macros/latex/contrib/pxcjkcat/README-ja)によると指定できるモードは4つです。

- forcecjk：upLaTeXのデフォルトと同じ。英語の文字以外は全て全角の和文扱い。
- prefercjk：Adobeの定めるCJK（中日韓）が包括する部分を和文扱いにする。と言いつつ上とあんまり変わらない。
- prefercjkvar：ギリシャ文字・キリル文字が欧文扱いになる。
- prefernoncjk：漢字・かななど最低限のCJK文字のみを和文扱いにし、それ以外は全て欧文扱い。

　ここではフランス語を欧文扱いしたいので、オプションに「prefernoncjk」を指定してやります。これで組んでみましょう。

{{< figure src="/img/43accent2/prefernoncjk.jpg" caption="" alt="欧文扱い成功" class="" >}}

　できたー！できたよおかあさーん！！これで文中にコマンドを使わずすっきり、かつ望む組版結果になりました。

#### 応用編
　プリセットの4つのモードはだいぶざっくりしたカテゴリ分けになりますが、実はpxcjkcatパッケージはもっときめ細かな指定をすることが可能です。  
　例えば上で使ったprefernoncjkモードは、本当に最低限しか和文扱いしないので、約物や記号は全部欧文扱いになってしまいます。なのでこういうことが起こります。

{{< figure src="/img/43accent2/noncjkwrong.jpg" caption="" alt="全角記号も全て横倒しに" class="" >}}

　パッケージの機能である`\cjkcategory`コマンドを使うことでこういった事態を回避できます。記号は普通に直打ちできるように和文扱いのままで、フランス語やスペイン語のアルファベットだけ欧文扱いしたい、という時は、プリアンブルで以下のようにしてやります。

```LaTeX
\usepackage[prefercjkvar]{pxcjkcat} %varモード。英語・ギリシャ・キリル文字だけ欧文扱いで、他は和文扱い
\cjkcategory{latn1}{noncjk} %Latin-1 Supplement（アクセントつきアルファベット）を欧文扱いに追加
```

　より詳しい使い方はブログで解説しています。プラス、この次ページの内容も参考にしてください。

#### 参考
- [BXbase／PXbase パッケージ [電脳世界の奥底にて]](http://zrbabbler.sp.land.to/pxbase.html#sec-pxcjkcat)
- [Unicode による文字の入力 [電脳世界の奥底にて]](http://zrbabbler.sp.land.to/unichar.html)
- [［改訂新版］upLaTeXを使おう - Qiita](http://qiita.com/zr_tex8r/items/5c14042078b20edbfb07)
- [UTF-8 で欧文文字を入力する ～inputenc パッケージ～ - Qiita](http://qiita.com/zr_tex8r/items/b40ca3478e4fe14868e5)
- [upLaTeX でアクセント付きのラテン文字などがうまく出力されないときの対処法｜Colorless Green Ideas](http://id.fnshr.info/2017/05/27/pxcjkcat/)
- [『その10：upTeXの和文カテゴリコードがアレ』](http://qiita.com/zr_tex8r/items/297154ca924749e62471#%E3%81%9D%E3%81%AE10uptex%E3%81%AE%E5%92%8C%E6%96%87%E3%82%AB%E3%83%86%E3%82%B4%E3%83%AA%E3%82%B3%E3%83%BC%E3%83%89%E3%81%8C%E3%82%A2%E3%83%AC)
