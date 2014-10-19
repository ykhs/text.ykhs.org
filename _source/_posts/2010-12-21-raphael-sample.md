---
layout: post
title: JavaScriptでSVGを描けるRaphaelを試し書き
---
<script src="/resources/post/2010-12-21-raphael-sample/raphael-min.js"></script>

JavaScriptでSVGが楽に描けるRaphaelというライブラリを試していたので少しメモ。  
ぱっと見てなるほどーって思える挙動を載せてみましたが、前面背面の配置を入れ替えたりとか、気の利く機能もある印象です。

Raphael公式はこちら。 [Raphaël—JavaScript Library](http://raphaeljs.com/index.html)

## 簡単に円など描いてみる

Raphaelのインスタンスを初期化してcircleメソッドを実行するだけ。

<div id="svg1" style="margin:30px 0 0;"></div>
<script>var el = document.getElementById('svg1');
	var r = Raphael(el, 100, 100);
	r.circle(50, 50, 40);
</script>

```javascript
// DOMで要素を取得
var el = document.getElementById('svg1');

// Raphaelインスタンスの初期化。パラメータは、
// 1. これから図形などを描く先となる要素
// 2. そこで確保する横幅
// 3. 同じく確保する高さ
var r = Raphael(el, 100, 100);

// そしてcircleメソッド。名のとおり円が描けます。パラメータは、
// 1. 中心点のx座標。
// 2. 中心点のy座標
// 3. 円の半径
r.circle(50, 50, 40);
```


## 属性操作

jQueryのattrメソッドライクに属性を操作できる模様。メソッドチェーンも同じ感覚で扱えるみたいでした。  
操作できる属性は公式ドキュメントにまとまってます  
<http://raphaeljs.com/reference.html#attr。>

<div id="svg2" style="margin:30px 0 0;"></div><script>var el = document.getElementById('svg2');
	var r = Raphael(el, 100, 100);
r.circle(50, 50, 40)
	.attr({
			'stroke': '#454545',
			'stroke-width': '5px',
			'fill': '#686868'
			});
</script>

```javascript
r.circle(50, 50, 40)
.attr({
	'stroke': '#454545',
	'stroke-width': '5px',
	'fill': '#686868'
});
```


## イベント

これもまたjQueryライクな仕様。同じように書いていけます。  
マウスが乗ったとき、離れたときのイベントを付けてみました。公式ドキュメントではここ。  
<http://raphaeljs.com/reference.html#events>

<div id="svg3" style="margin:30px 0 0;"></div><script>var el = document.getElementById('svg3');
	var r = Raphael(el, 100, 100);
r.circle(50, 50, 40)
	.attr({
			'stroke': '#454545',
			'stroke-width': '5px',
			'fill': '#686868',
			'cursor': 'pointer'
			})
.hover(function (e) {
		this.attr({
			'fill': '#8a8a8a'
			})
		}, function (e) {
		this.attr({
			'fill': '#686868'
			})
		});
</script>

```javascript
// イベントもメソッドチェーンでつなげて書ける。前半は上と大体同じ。
// 実際にイベントを与えているのは10行目、.hover(function ～ のところから。
r.circle(50, 50, 40)
.attr({
	'stroke': '#454545',
	'stroke-width': '5px',
	'fill': '#686868',
	'cursor': 'pointer'
})
.hover(function (e) {
	// マウスが乗ったら塗色を変える
	this.attr({
	  'fill': '#8a8a8a'
	})
}, function (e) {
	// マウスが離れたら塗色を戻す
	this.attr({
	  'fill': '#686868'
	})
});
```

## アニメーション

あと、アニメーション。このときにonAnimationのイベントを登録してあると、アニメーションの都度、フィードバックが得られるようでした。そこで拾った情報で他の要素を操作したり情報を出したりっていうのが出来そうです。

<div id="svg4" style="margin:30px 0 0;"></div><script>var el = document.getElementById('svg4');
	var r = Raphael(el, 640, 100);
	var p = r.path('M0,50L80,50').attr({
			'stroke-width': '3px',
			'stroke-linecap': 'round',
			'stroke': '#ff6666'
			});
var c2 = r.circle(80, 50, 5).attr({
		'stroke': 'none',
		'fill': '#454545'
		});
var c = r.circle(50, 50, 40).attr({
		'stroke': '#454545',
		'stroke-width': '5px',
		'fill': '#686868'
		}).onAnimation(function () {
			var rad = Raphael.rad(c.attr('rotation'));
			var x = c.attr('cx') + Math.sqrt(30 * 30) * Math.cos(rad);
			var y = c.attr('cy') + Math.sqrt(30 * 30) * Math.sin(rad);
			p.attr({
path: 'M0,50L' + x + ',' + y
});
			c2.attr({
				'cx': x,
				'cy': y
				});
			}).toBack();
</script><input type="button" value="start" onclick="
c.stop().animate({
'cx': '540',
'rotation': '540',
}, 2000, 'bounce', function () {
c.animate({
'cx': '50',
'rotation': '-540',
}, 3000, '&#038;lt&#038;gt');
});
">

```javascript
var el = document.getElementById('svg4');
var r = Raphael(el, 640, 100);

// パス
var p = r.path('M0,50L80,50').attr({
	'stroke-width': '3px',
	'stroke-linecap': 'round',
	'stroke': '#ff6666'
});

// 小さい円
var c2 = r.circle(80, 50, 5).attr({
	'stroke': 'none',
	'fill': '#454545'
});

// 大きい円。アニメーションさせる要素。
var c = r.circle(50, 50, 40).attr({
	'stroke': '#454545',
	'stroke-width': '5px',
	'fill': '#686868'
}).onAnimation(function () {
	// onAnimationイベント時に得られる情報を使って上のパスと、小さい円を動かしています。
	var rad = Raphael.rad(c.attr('rotation'));
	var x = c.attr('cx') + Math.sqrt(30 * 30) * Math.cos(rad);
	var y = c.attr('cy') + Math.sqrt(30 * 30) * Math.sin(rad);
	p.attr({
		path: 'M0,50L' + x + ',' + y
	});
	c2.attr({
		'cx': x,
		'cy': y
	});
}).toBack();

// アニメーション。パラメータは、
// 1. 目標とする属性値
// 2. それに費やす時間
// 3. イージング
// 4. アニメーション完了時のコールバック
c.stop().animate({
	'cx': '540',
	'rotation': '720',
}, 2000, 'bounce', function () {
	c.animate({
		'cx': '50',
		'rotation': '-720',
	}, 3000, '&lt;&gt;');
});
```
