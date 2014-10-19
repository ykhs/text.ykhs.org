---
layout: post
title: jQuery UI で要素が徐々について来るドラッグ挙動プラグイン
---

このプラグインは書き直されていて、以下が新しい内容となります。

慣性ドラッグの jQuery UI プラグインを書き直した  
<{{ site.url }}{% post_url 2011-09-26-jquery-ui-phantomDrag-rewrite %}>

## 経緯

jQuery UI に draggable っていうのはあるけど、これは、マウスにぴったり付いてくる。この動きが普通だしこれでいいんだけど、ドラッグに対して少し遅れてついてくるような、ふわっとした動き。こいうのがあると触ったときの気持よさっていうのも向上する。

あと、ドラッグ操作を行った時、必ずしもドラッグ対象の要素の位置が動くっていう反応を返す場面ばかりとは限らない。レバーみたいなパーツをドラッグすると、レバーは傾いた反応を見せて、また別の要素が動く。という仕掛けになるかもしれない。その辺も柔軟に対応しとく。

## サンプルとか

こちらの記事を参考に、GitHub Pages を使ってサンプルを上げました。これ便利だ

GitHub 上に ページを作成する | Tanablog  
<http://blog.kaihatsubu.com/?p=1836>

サンプル  
<http://ykhs.github.com/jquery.ui.phantomDrag/sample.html>

説明書  
<http://ykhs.github.com/jquery.ui.phantomDrag/readme.html>

## 何をしてるのか

要素をドラッグして、マウスにゆっくり近づく動きをしているつもりの値を、実際の動きを伴わずに .data() で拾える値として書き出しています。そして、ドラッグ中の状態を示す各種カスタムイベントがあるので、それらに対して .bind() を使いつつ値を取り出して利用してもらうという想定。

例えば、 “phantomdrag-move” というカスタムイベントの定義があって、これは要素の計算上の位置が移動するたびに発火します。これに bind して jQuery の .data() を使って “phantomdrag–x” というX座標の現在位置の値を拾う。これをそのまま bind のコールバック内で、$(event.target).css(‘left’, x); とかすれば普通にドラッグに追従する要素になります。

ただ、要素をドラッグしたらマウスについて来る。みたいな動きには決め付けず、コールバック内で好きにしてもらえるように作ってみたので、ちょっと値の計算を加えたり、別の要素を動かすことにも使ってみると面白いと思います。

ykhs/jquery.ui.phantomDrag – GitHub  
<https://github.com/ykhs/jquery.ui.phantomDrag>
