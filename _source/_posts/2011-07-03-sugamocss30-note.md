---
layout: post
title: 第30回 Sugamo.css へ行ってきた
---

Sugamo.css という、[Sig.さん](http://twitter.com/#!/sigwyg "Sig. (sigwyg) on Twitter")の主催されている Web フロントエンドな集まりへ行ってきたのでメモ。発表の辺りとかを中心に、自分も適当に作業しながらだったりしたので聞き取っていたところだけになっています。順序も少し、うろおぼえかもしれません。

第30回 Sugamo.css : ATND  
<http://atnd.org/events/17263>

## 発表メモ

### [@yomotsu](http://twitter.com/#!/yomotsu "Akihiro Oyamada \(yomotsu\) on Twitter") さん

Adobe Illustrator からの SVG 書き出し

- 座標とかの情報は小数点第何位までというのがコントロールできる
- Web 用に保存を使うとレイヤーとかが消えてしまう
- 別名に保存を使えば g 要素でレイヤーが残る。 id はレイヤーの名前になる。
- 小数点を丸めればファイルサイズの削減ができる
- DW で SVG 要素を記述するための補完機能とかライブビューとか載ってる (CS 5.5)
- （全体的に結構最近めな Adobe CS の機能かも）

### [@ykhs](http://twitter.com/#!/ykhs "ykhs \(ykhs\) on Twitter") （自分）

慣性ドラッグの jQuery プラグイン紹介

- これ。 SAMPLE – jquery.ui.phantomDrag.js
  <http://ykhs.github.com/jquery.ui.phantomDrag/sample.html>

- 自己紹介のつもりで、さっと出せるもので話そうとしたつもりだったけど、やっぱり難しい。慣れとか練習とかは要る。
- 何をどこまで話すか。簡単にデモを見せただけだったのだけど、ソースとか見せながら突っ込んだ話もしてフィードバックを頂ける流れを作れたら良かったかもしれない。

### [@neotag](http://twitter.com/#!/neotag "neotag \(neotag\) on Twitter") さん

Sass について。RubyGems の compass とか

- （Sass と聞いて黙々試してみるモードになってたので、たぶんこれ以降のいくつかの発表が抜けてしまっているかと思います。）
- “sass –watch .” とすれば input.scss:output.css の記述を省略できて楽。
- compass 便利。config.rb を用意して –style :expanded の設定とかを統一できる。チームでの利用に必須っぽい。
- CSS スプライト作成支援機能もある模様。
- Web に上がっている公式ドキュメントの内容が古い。自分で調べて使う感じ。

### [@takazudo](http://twitter.com/#!/takazudo "Takeshi Takatsudo \(takazudo\) on Twitter") さん

GAE で作ってる物紹介

- GAE で作り中のものを少し見せていただけた。
- 僕も GAE とか heroku とかそれ系なのいじってみたいな～欲が上がりました。

### [@yomotsu](http://twitter.com/#!/yomotsu "Akihiro Oyamada \(yomotsu\) on Twitter") さん（2）

最初のは前振りで、本番。SVG で地図

- SVG Animation でかっこよく動く地図。
- viewBox の話。SVG 画像を表示する原点と横幅・高さを決められる？

### [@taku\_eof](http://twitter.com/#!/taku_eof "Taku Watabe \(taku_eof\) on Twitter") さん

WeakMap の話

- オブジェクトをキーとした値を定義できる
- そのキーとなるオブジェクトがガベージコレクトされてしまう可能性があるため for in とかでキーの列挙はできない

## まとめ

- SVGで地図を扱うというのはやってみたいし、理にかなってる。Gif画像をイメージマップ切って扱うとかよりスマートだと思う。Raphaël とか使ってレガシーブラウザも考慮してねっていうのは必要だろうけど。
- Sassはメンバー間のコーディングスタイルの違いを吸収、資産の積み重ねをしていくのにとても良いな～とは感じていて、さらに今回伺った compass でプロジェクト設定みたいなことも出来るようになっていてますます良いな～と思った。

