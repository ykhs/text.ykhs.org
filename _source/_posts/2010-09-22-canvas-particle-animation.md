---
layout: post
title: HTML5のcanvas要素でパーティクルアニメーション
---

## 動いてる様子はこちら

（2011/2/28 github やめて jsdo.it から呼ぶようにしました）

<script type="text/javascript" src="http://jsdo.it/blogparts/zehA/js?view=design"></script><p class="ttlBpJsdoit" style="width: 465px; margin: 0; text-align: right; font-size: 11px;"><a href="http://jsdo.it/ykhs/zehA" title="particlePractice">particlePractice &#8211; jsdo.it &#8211; share JavaScript, HTML5 and CSS</a></p>

## 今回の狙い

前々からパーティクルアニメーションになんとなく興味があったのだけど、何もせず終い。nettutsなんかを見ていると既にHTML5のかっこいいデモが沢山作られていて刺激を受けたので、自分でもHTML5のcanvasを使ってパーティクルアニメーションを作ってみました。

作って見せておいてなんですが、nettutsで適当な記事から飛んだ先の作品のソースを沢山読んだ方が勉強になりそうです。影響を受けてる元もバレるのですが、この記事とか。

21 Ridiculously Impressive HTML5 Canvas Experiments | Nettuts+  
<http://net.tutsplus.com/articles/web-roundups/21-ridiculously-impressive-html5-canvas-experiments/>

## 動きとか

canvasでのアニメーションは基本、以下の繰り返しで作ってます。

1.  絵を描く
2.  背景色で塗りつぶす
    1.  このときにアルファ値も持たせると残像や軌跡を描いたような表現に

3.  少し動かした絵を用意する
4.  1に戻る

4番の辺りで行う円運動の計算やら、次のフレームで図形を描く位置の算出やらは『Flash Math & Physics Design』で聞きかじった知識を記憶の中からそれとなく紡いで織り込んでます。
