---
layout: post
title: Chrome で試せる Shadow DOM
---
Chrome の about:flags に “Shadow DOM を有効にする” という項目が出来ている。たぶん、バージョン 19 くらいから。

Shadow DOM というのは W3C WebApps Working Group の方で提案されている Web Components と呼ばれる、 HTML をうまく部品化する仕組みを構成する要素の一つで（言葉使いとかあってるか微妙。）ブラウザを通じて Web サイトのレンダリングを行った際に現れる見かけ上の文書ツリー。

あくまで見かけ上であり、実際には Shadow DOM はそれを保持している文書ツリーとは別の空間に存在していて、Shadow DOM には Shadow DOM のルート要素的なものがある。そのため文書ツリー側で定義したスタイルは適用されないし、Shadow DOM 内で定義したスタイルも文書ツリーには影響しないなどの特徴がある。document.querySelectorAll() とかも効かなくて、[Shadow DOM のルート].querySelectorAll() という風にアクセスする。

それで冒頭の通り、Shadow DOM の機能が少しだけ使えるようになってきている。
というわけで Shadow DOM の挙動がちょっとわかるかもしれない簡単なデモを書いてみた。

Shadow DOM Sample — Gist  
<https://gist.github.com/3027432>

ほとんど、W3C の下記の文書に載っていたサンプルを参考にしている。  
ここの例では new ShadowRoot() で ShadowRoot オブジェクトを生成しているけど、現状 new WebkitShadowRoot() と、プレフィクスが必要だった。

Shadow DOM  
<http://www.w3.org/TR/shadow-dom/#shadow-dom-example>

それで、必要な設定を行なった Chrome で上記のデモを開くと JavaScript を通じて生成した Shadow DOM のレンダリング結果が得られる。文書ツリー側で定義したスタイルが効いていないことや、document.querySelectorAll('h1') とかコンソールで打っても取得対象にならないことが確認出来ると思う。

Chrome で必要な設定は以下の通り。

![](/resources/post/2012-07-01-chrome-shadowdom/chrome_shadowdom_1.png)
about:flags から上記のオプションを有効にする。  
style scoped 属性も使っているのでこちらも有効化。

![](/resources/post/2012-07-01-chrome-shadowdom/chrome_shadowdom_2.png)
Chrome Developer Tools の Web インスペクタで Shadow DOM を表示出来るようにする設定。…を、Chrome Developer Tools に表示するための設定。

![](/resources/post/2012-07-01-chrome-shadowdom/chrome_shadowdom_3.png)
それから Chrome Developer Tools 右下の歯車ボタンを押すと現れる設定パネルの中に、Web インスペクタで Shadow DOM を表示するか否かの設定が現れるのでこれも有効化。

![](/resources/post/2012-07-01-chrome-shadowdom/chrome_shadowdom_4.png)
すると Shadow DOM が有効になってさらに、Web インスペクタにも Shadow DOM が表示されるようになる。見かけ上の DOM ツリーというものがどういうことか、実際の挙動もこれで確認出来る。

## 参考

Introduction to Web Components  
<http://www.w3.org/TR/2012/WD-components-intro-20120522/>  
Web Components に関する W3C の文書

Introduction to Web Components - DOM ECMAScripting  
<http://domes.lingua.heliohost.org/webapi/intro-webcomponents1.html>  
Introduction to Web Components の翻訳

Shadow DOM  
<http://www.w3.org/TR/shadow-dom/>  
Shadow DOM に関する W3C の文書

Web Components - Google+  
<https://plus.google.com/103330502635338602217/posts>  
Web Components に関する Google+ ページ

