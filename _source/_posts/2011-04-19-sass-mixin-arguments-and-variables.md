---
layout: post
title: Sass（SCSS）で引数付きの Mixins と変数計算を試す
---

## 粗筋

[前回の記事]({{ site.url }}{% post_url 2011-04-12-sass-on-mywebsite %})でこのサイト用に Sass
を試してみたのだけど、簡単なサイトなのであっさりした感じで終了。引数付きの Mixins だとか変数の計算とかも試してみたかったので、[960
Grid System](http://960.gs/) の CSS をベースにカラム幅を自動算出してくれる Grid CSS
というのをお題にやってみることにしました。

試したかったのは上記の引数とか計算とかなので、実用性の方はあまり気にしてません。展開における挙動の確認や、何かしらのインスピレーションになれば幸いです。

「Sass Grid」とかで検索してみると、既に同じ事は結構考えられているっぽいです。

## 結果

Mixins の定義を詰めた \_grid.scss と、それを利用している style.scss。あと、展開後の style.css です。

960 Grid System Using Sass. — Gist https://gist.github.com/925516  
<https://gist.github.com/925516>

## サイト横幅、カラム数、カラム間マージンを最初に定義

[この style.scss
ファイル](https://gist.github.com/925516#file_style.scss)の上の方に書いてあるように、最初に $contentsWidth （サイト横幅）、$numberOfColumns （カラム数）、$gutterWidth （カラム間マージン）を定義しました。カラムの設定を @include で呼ぶ度に、これらの値を引数として渡してやることで然るべき横幅を計算してあげましょう。という仕組みです。

## 上記の定義を引数に渡して @include

[同じく style.scss
ファイル](https://gist.github.com/925516#file_style.scss)の少し下から始まってますが、一番親のラッパー的な div には grid-container を、第1引数にサイト横幅、第2引数にカラム間マージンを渡して @include。

各カラムでは grid を、第1引数にカラムの専有枠数、第2にサイト横幅、第3はカラム数、第4でカラム間マージン、と渡してやりつつ
@include します。  
それで、第1引数の専有枠数なのですが、最初に定義したカラム数を超えた値も指定出来てしまいます。サイト横幅の上限を超えないようにする方法は思いつかなかったので、そこは、止めてね。と言うしかないですね。

## 出来上がり

こんな CSS ファイルが出来ました。

960 Grid System Using Sass. — Gist https://gist.github.com/925516\#file\_style.css  
<https://gist.github.com/925516#file_style.css>

ここでは12カラムの設定にしていて、[960 Grid System
で同じ設定をした場合のジェネレータ結果](http://grids.heroku.com/grid?column_width=60&column_amount=12&gutter_width=20)とも同様なものを展開することが出来ました。

今回はサイトの横幅、カラムのマージンといった数値を引数に投げ込むとグリッド組んであげるよ。っていう仕組みを作ってみたわけだけど、Sass のドキュメントを眺めていると色周りの機能もだいぶ充実してる模様。  
何か1色ベースカラー決めて、引数に投げるとかっこいい、或いはかわいい配色パターンを展開してあげるよ。っていうのも出来るかなーと思っていたり、まぁ、気が向いたら。
