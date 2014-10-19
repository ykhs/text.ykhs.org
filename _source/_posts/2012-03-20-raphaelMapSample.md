---
layout: post
title: Raphaël を使った SVG による地図表示
---
Raphaël に path() メソッドというのがあって、SVG 仕様のパスデータを文字列として渡すとそれに従って図形を描画してくれます。（path 要素の d 属性として扱ってくれます。）これを使って日本地図の SVG データを出力してみました。

Raphaël Sample - Map of Japan  
<http://ykhs.github.com/raphaelMapSample/>

画が出るだけなら SVG をそのまま貼りつけてもいいのだけど、Raphaël オブジェクトとして SVG を生成すると click() メソッドを始めとしたユーザー側で起こるイベントのハンドリングや、座標計算、アニメーションなどの機能をJavaScript から利用出来るといった恩恵が受けられるので、JavaScript 側から色の設定やイベントハンドリング、アニメーションをさせたりっていうのを試しています。

最初、各都道府県の要素をクリックしたときに Raphaël のアニメーション機能を使って .animate({x: 100}) のような書き方で移動させようとして動かないなーとか思っていたのですが、SVG の path 要素にそもそも x 属性などが存在しないことに気づいて、.animate({transform: "t100,0"}) のような書き方に変更をしました。

Raphaël の transform には変換用文字列を渡せばいいようです。-> [Raphaël Reference](http://raphaeljs.com/reference.html#Element.transform)

## 使用素材

日本地図のパスデータとしてこちらのデータを使用しています。  
<http://www.kabipan.com/geography/whitemap/index.html>

都道府県名のフォントはこちらのはんなり明朝です。  
<http://typingart.net/index.html>
