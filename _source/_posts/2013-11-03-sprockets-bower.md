---
layout: post
title: SprocketsとBowerで作業環境を作る
---

このライブラリちょっと試したいとかあの挙動確かめたいとか、そういう簡単な作業環境が楽に準備できるようなものをSprocketsとBowerを利用して作ってみた。

<https://github.com/ykhs/workbench>

下の手順でサーバーが起動して `http://localhost:9292/` でサイトが見られるようになる。

```text
$ git clone https://github.com/ykhs/workbench.git
$ cd workbench
$ rake setup
$ rake server
```

ライブラリを追加したいと思ったら `bower install` して `assets/js/lib.coffee` にSprocketsの `require` ディレクティブを追記する。

```text
$ bower install momentjs
$ echo "#=require momentjs/moment.js" >> assets/js/lib.coffee
```

`assets/js/lib.coffee` には記述サンプルも兼ねて、jQuery, Underscore, Backboneの3点を最初から読むようにしてある。  

```coffeescript
#assets/js/lib.coffee

#=require jquery/jquery
#=require underscore/underscore
#=require backbone/backbone
```

もちろん、`bower.json` の `dependencies` の方にもこれらは依存ライブラリとして記述してある。  
素の `bower install` は `rake setup` のタスク内で `bundle install` と一緒に実行されるようにしていて、配置については、同梱した `.bowerrc` に従って `assets/vendor` 配下に置かれる。

こんな感じの配置になる。自分のスクリプトは `assets/js/main.coffee` に書いていくという具合。

```text
assets/
├── css
│   ├── lib.scss
│   └── main.scss
├── js
│   ├── lib.coffee
│   └── main.coffee
└── vendor
    ├── backbone
    ├── jquery
    └── underscore
```

同じ要領でCSS用にも `assets/css/lib.scss` と `assets/css/main.scss` を用意している。

また、 `http://localhost:9292/test` でmochaによるテストも実行できる。  
テストコードは `assets/js/tests/*.coffee` へ適当に書いておけば、 `assets/js/test.coffee` に記述しておいた `require_tree` ディレクティブが拾ってくれる。  
単純に自分が慣れているという理由でmocha, expect, sinonを選択して `bower.json` に入れておいた。

テンプレートエンジンは、特にこだわりなくslimを使ってる。

bowerいいなーとは感じていたものの、 `bower install jquery` とかやっていい感じにパッケージを所得したのに `<script src...>` ってHTMLにいちいち書かなくちゃいけないのがなんとなく腑に落ちなくて、まあ仕方ないんだけど。Sprockets使えばそういう気持ちにならないだろうと思って試してみて、割といい感じはしている。

## 参考

- [昨今の自分用Webアプリケーションひな形 - naoyaのはてなダイアリー](http://d.hatena.ne.jp/naoya/20130503/1367581629)
- [Webアプリのモックアップ作業土台を作る その1 - cu39's diary](http://cu39.hateblo.jp/entry/2013/07/02/183935)
