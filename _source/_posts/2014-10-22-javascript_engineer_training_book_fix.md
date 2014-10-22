---
layout: post
title: JavaScriptエンジニア養成読本Backbone.js特集の訂正
---

先日発売された[JavaScriptエンジニア養成読本]((http://gihyo.jp/book/2014/978-4-7741-6797-8))ですが、Underscore.jsのバージョンが執筆時の 1.6.0 から 1.7.0 に変わっている関係で、現状だといくつかのコードが動作しないようでした。確認漏れですすみません…。

`_.template()`が常にコンパイル済みのテンプレートを持った関数を返すようになった関係で文中のサンプルにある次のようなコードが動かなくなっています。

```js
var html = _.template(htmlTemplate, data);
```

正しくは次のような感じのコードにする必要があります。

```js
var compiled = _.template(htmlTemplate);
var html = compiled(data);
```

一応、掲載されているコードで修正が必要なものについては正しい例をこちらに載せておきます。

- 特集1 第4章 リスト3

    <https://gist.github.com/ykhs/f64df63c8e223c3d00aa>

- 特集1 第4章 リストA

    <https://gist.github.com/ykhs/39048d0aff620ec328d4>

- 特集1 第4章 リスト13

    <https://gist.github.com/ykhs/d83ba1e1e4c42cf287be>

- 特集1 第6章 リスト8

    <https://gist.github.com/ykhs/04e772788e17b46a1411>

- 特集1 第7章 リスト1

    <https://gist.github.com/ykhs/f2ab66e8a67be16781d3>

- 特集1 第7章 リスト5

    <https://gist.github.com/ykhs/3db59c4ad4c4604af198>

- 特集1 第7章 リスト20

    <https://gist.github.com/ykhs/80fae0311cdf58002e85>

[JavaScriptエンジニア養成読本［Webアプリ開発の定番構成Backbone.js＋CoffeeScript＋Gruntを1冊で習得！］：書籍案内｜技術評論社](http://gihyo.jp/book/2014/978-4-7741-6797-8)
