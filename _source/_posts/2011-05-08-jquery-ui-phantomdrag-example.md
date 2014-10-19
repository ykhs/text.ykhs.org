---
layout: post
title: 慣性ドラッグプラグインを使ったスライダーの作例
---

このプラグインは書き直されていて、以下が新しい内容となります。

慣性ドラッグの jQuery UI プラグインを書き直した  
<{{ site.url }}{% post_url 2011-09-26-jquery-ui-phantomDrag-rewrite %}>

前に、[慣性の付いたマウスドラッグの挙動作成を助けるようなプラグイン]({{ site.url }}{% post_url 2011-03-06-jquery-ui-phantomdrag %})を作ったのですが、これを使ったごく簡単な作例で、もう少し、実際にありそうな作り物に近いものを載せたかったので書いてみました。

## サンプルページ

Sample っていうところに並んでいる黒い四角の物体たちをマウスドラッグで動かせます。

SAMPLE – Slider using jquery.ui.phantomDrag.js  
<http://ykhs.github.com/jquery.ui.phantomDrag/sample_slider.html>

## 主なコード

これがプラグインを読み込んだ上で実際の挙動を実現しているコードです。\
ここでやってることだけなら、jQuery UI Widget なんて使う必要はなかったりもしますが、簡単な例ということで。

けれども、込み入った UI
なんかを作っているとプラグイン内部のメソッドに外からこのタイミングでアクセスしたい。というのが出てきたり、そのためのメソッドを追加するための継承をしたくなってきたりとかするのではないかと。ということで、そういうことのし易い形で最初から作っとこう、という風になっています。

<script src="https://gist.github.com/960624.js?file=gistfile1.js"></script>
