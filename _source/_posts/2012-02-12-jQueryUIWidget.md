---
layout: post
title: jQuery UI Widget について
---
jQuery UI Widget について簡単に書いておいてみたくなった。

まず jQuery UI という jQuery 公式の UI 作成拡張キットみたいなものがあって、それの基板となっているモジュールが jQuery UI Widget。いわゆる jQuery プラグインと呼ばれるものを作るにあたってより多くの機能の恩恵が受けられる。この jquery.ui.widget.js だけ使うなら minify されたもので一桁 KB と、サイズも小さい。

jQuery プラグインというものを普通に作ろうとするとたぶん、なにか初期処理を行なったら、あとはイベントに応じて勝手に動くというものが出来上がると思う。

簡単なスライドショーとかはそれで十分なんだけど、例えば jQuery プラグイン同士が連携しあって動くとか、別に jQuery なんとかではなく何でも、自分で書いたコードからこのタイミングでプラグイン内のこのメソッドにアクセスしたいとか。あとは一時的に機能を無効化しておきたいとかもあったりして、そういう辺りのことをサポートしてくれる。

上述の、普通に作る、というのをやるとたぶんパブリックメソッドすら定義出来なくて、やりたかったら結構トリッキーなことをしないといけない。この辺は jqueryboilerplate.com にある例がわかりやすいと思った。 $.fn[pluginName] に定義した関数内で、受け取った要素に対して $.data(); を使って生成したインスタンスを埋め込んでいる。プラグイン内のメソッドとかにアクセスしたかったら、$.data() に埋まってるインスタンス経由で行けばいい。

jQuery Boilerplate  
<http://jqueryboilerplate.com/>

例えば jQuery Boilerplate のやり方で作ったプラグインに、 hello() メソッドがあってそれにアクセスしたい場合はこのような感じになる。

```javascript
$('#great-element').greatPlugin();
$('#great-element').data('greatPlugin').hello();
```

これが jQuery UI Widget だとこうなる。実際、こちらも $.data() でインスタンスを埋め込んでいるのだけど、いくらか判りやすい方法を提供している。

```javascript
$('#great-element').greatPlugin();
$('#great-element').greatPlugin('hello');
```

この辺りの話はほんの一部で、他にも、「便利にしといてやったからこう書いておけ。」というようなガイドラインが示されている。設定の初期値は options プロパティに書くこと。コンストラクタは \_create() に定義すること。（一応、パブリック・プライベートメソッドの区別もサポートしてる。）カスタムイベントの発行と、対するコールバックの定義方法。（this.\_trigger('event') とする。 bind('event') してもよいし、プラグインの初期化時に渡す引数オブジェクトで event: function() {} としてもよい。）

その他便利機能、登録したイベントの無効化と復帰も disable(), enable() で行える（CSS の class 属性値まで変えてくれる。）とかがあったりして色々と気が利いている。

初期化しっぱなしでなく、状態が変化して、オブジェクト同士相互に協調するような UI を提供するときにはこのくらいのものが入用になってくるし、積み重なった知恵や工夫をフレームワークとしてまとめて jQuery の使用感で扱えるようにしてくれている辺り有益と感じてる。

jQuery UI Development & Planning Wiki / Widget factory
<http://wiki.jqueryui.com/w/page/12138135/Widget-factory>  

ドキュメントはここ。

demos/widget/default.html at master from jquery/jquery-ui &#8211; GitHub  
<https://github.com/jquery/jquery-ui/blob/master/demos/widget/default.html>

ダウンロードしたファイルの中に、Widget のデモも含まれている。

