---
layout: post
title: Sass linear-gradient() Mixin 2012 Autumn
---

[クロスブラウザな css3 linear-gradient が面倒になりそうな件について - ほむらちゃほむほむ](http://t-ashula.hateblo.jp/entry/2012/08/27/145535)

上記の記事を参考に、linear-gradient() の Sass mixin を書いてみました。

[linear-gradient Sass Mixin — Gist](https://gist.github.com/3690526)

参考記事中の “2012 年の秋冬に待ち受ける事態 - IE10 での linear-gradient” の例にあたる書式で出力できるようにしています。一応 Windows 8 Release Preview に載っている IE10 で、 vendor-prefix を持たず to キーワードありの記述が有効であることも、ごく簡単に確認済み。

side-or-corner の指定は従来通りの top でも to キーワードのついた to bottom でも、 vendor-prefix のそれぞれ（といっても今は有りか無しかで分かれていますが）に対応した記述に変換します。45deg みたいな angle による指定もそれぞれ同様に変換しますが、従来通りの、x 軸正方向から反時計回りで数える指定方法を期待する作りになっています。今はまだ、こっちの方が慣れてるかなーと思って。けど、どっちがよいのだろ。

color-stop は Sass 3.2.0 から対応した可変長引数を利用しているので、複数の color と position の指定が自由に行えます。単純に @incluce linear-gradient(top, black, white); にしても、複数色で linear-gradient("to bottom", #1e5799 0%,#2989d8 50%,#207cca 51%,#7db9e8 100%); みたいにしても OK。


