---
layout: post
title: 慣性ドラッグの jQuery UI プラグインを書き直した
---
[前に作った、要素のドラッグに慣性っぽい挙動をつける jQuery UI プラグイン]({{ site.url }}{% post_url 2011-03-06-jquery-ui-phantomdrag %})をだいぶ書き直した。  
併せて、Web に上げたドキュメントもすっかり新しくしています。

jquery.ui.phantomDrag.js  
<http://ykhs.github.com/jquery.ui.phantomDrag/document/>

これは、プラグインを実行した要素をドラッグすると mousemove みたいな頻度でカスタムイベントが発生するので、それに .bind() して値を取得することで、現在のマウス位置より遅れた位置の座標が手に入ったりするというものでした。  
ふわっとした動きのスライダーなんかを作るときに便利です。

## 前の版のよくないと思ったところ

カスタムイベントにバインドして、座標の取得は jQuery.fn.data() を使うっていうところにかなり回りくどさを感じていました。

```javascript
$('#element').phantomDrag();

$('#element').bind('phantomdrag-move', function (e) {
  console.log($('#element').data('x');
})
```

## 今の版のよくなったと思うところ

プラグインを実行するときにコールバック関数を指定するように変更しています。  
上記と同じく mousemove 的な頻度でドラッグ位置の情報を取りたい時には step というコールバック関数があるので、それを指定。  
そして第二引数で、ドラッグした際の位置に関する情報をオブジェクトで受け取るようにしました。

これで、少しシンプルになったんじゃないかと。

```javascript
$('#element').phantomDrag({
  step: function (e, res) {
    console.log(res.currentX);
  }
});
```

ふわふわしたドラッグ挙動つけたいだけなのに、このカスタムイベントに .bind() してください。で、値は jQuery.fn.data() で取得してください。とか、どうもルーブ・ゴールドバーグチックだし、プラグインと利用者を繋ぐ窓口を利用者にコントロールできないレイヤーで煩雑に規定してしまってるのがよくなかったのでは、とか考えてる。
