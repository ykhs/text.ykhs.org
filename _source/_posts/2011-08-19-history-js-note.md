---
layout: post
title: History.js メモ
---
HTML5 History API の polyfill として機能するライブラリ &#8220;History.js&#8221; を解釈してみた点についてのメモです。

balupton/history.js &#8211; GitHub  
<https://github.com/balupton/History.js/>

スクリプトのロード方法については GitHub に置かれている README が充実しているので基本的にそちらを参照するのが良いです。  
&#8220;Download &#038; Installation&#8221; の項になります。

## History オブジェクト

スクリプトをロードすると History オブジェクトが利用可能になります。ブラウザが提供する history オブジェクトとは大文字・小文字違いになっていて、History.js が提供する機能はこの History オブジェクトから利用します。

次に、たぶんよく利用するのではないかというメソッドなどについて。

## History.pushState()

ブラウザの履歴エントリに新しい URL を加える事ができます。

HTML5 History API における history.pushState() と同じように、以下の引数を渡すことが出来るため history.pushState() と同じ使用感で扱えます。

1. 第一引数: state object &#8211; popstate イベントオブジェクトの state プロパティへ渡すオブジェクト
2. 第二引数: title &#8211; 遷移先の title
3. 第三引数: URL &#8211; 遷移先の URL

history.pushState() に未対応のブラウザでは、このメソッドを実行した際に、URL の末尾に #hoge.html?&#038;\_suid=229 といったような location.hash が付与されます。たぶん popstate イベントの代わりに hashchange イベントを用いているためかと思われます。そんなことを述べている説明も README にありましたが、これで合ってるかな。

また、history.pushState() と比べると両者の pushState() 実行時には

1. 第二引数の title が title 要素の値として反映される。
2. popstate イベントの発火を伴う。

といった違いが見られました。

## History.replaceState()

こちらも、History API における replaceState と同じで、URL を書き換えたいが、History.pushState() のようにブラウザの履歴エントリを残さずに行いたい。といったときに使います。

## History.getState()

現在の履歴エントリの情報を取得します。返り値はオブジェクトになっており、様々な値が格納されているのですが実際に使うのは、data, title, url プロパティ辺りでしょうか。

History.pushState() を実行してブラウザの履歴エントリに格納した際の3つの引数と対応しており、渡した引数の第一引数は data. 第二引数は title. 第三引数は url を参照することでそれぞれ取得することができます。

## statechange イベント

参照する履歴エントリに更新があった場合に送出されます。History.pushState() が実行されたり、それによって登録された履歴エントリをブラウザの「次へ」「戻る」機能で再度踏んだ場合とかですね。

History API が提供する popstate イベントとは別名の statechange というイベント名になっています。

## History.Adapter.bind / History.Adapter.trigger / History.Adapter.onDomLoad

左からイベントの登録、イベントの強制発火、DOM 構築完了時のコールバック関数登録メソッドですが、それぞれ、一緒に利用するフレームワークに合わせてその処理を移譲するように出来ているようです。

history.adapter.${指定フレームワーク}.js という .js ファイルもロードする必要があるのですが、ここで例えば history.adapter.jquery.js をロードしていれば、

- History.Adapter.bind: は jQuery の .bind()
- History.Adapter.trigger: は jQuery の .trigger()
- History.Adapter.onDomLoad: は jQuery の $(function(){&#8230;})

と、対応するようです。

## 便利なところ

### history.pushState() 未対応ブラウザに対する同等機能+便利機能の提供

history.pushState() に見対応なブラウザに対しても、同じ使用感でこの機能が使えるのは快適でした。

History.pushState() 第二引数の title が title 要素に反映される点は、遷移先の title が判っていれば a 要素の title 属性に仕込んでおいたり、data-\* 属性に仕込んでおいたり JavaScript のソースに書いておいたりしたのを使えば、自分で Ajax のレスポンスから値を取得して title 要素のテキストを差し替えるといった手間が省けて便利だなぁと感じました。

popstate イベントの発火も伴う点についても、click イベントのデフォルト挙動をキャンセルして popstate イベントの強制発火というのを自分で行うことが多いのではないかと考えると、これもまた便利なものだと感じます。

### History.getState() による現在の履歴エントリ情報の取得

一応、現在の履歴エントリの情報を得る手段としては、HTML5 History API における history.state プロパティの参照によっても行えます。

しかし、history.pushState() に対応しているけれど history.state には対応していない。といったブラウザ（Safari5）も存在しており、History API に全く未対応なブラウザも含めてこの辺りの違いを吸収し、どのブラウザでも同じ情報を取得できるこの機能はとても便利です。

また、history.state プロパティに格納されている値は、history.pushState() の第一引数に渡した値のみであり、History.getState() によって得られるオブジェクトには History.pushState() に渡した第三引数までの全ての値が得られます。

ただ、この点については特別にすごい！といった感想ではなく、基本的には第一引数の state 情報を基にした画面更新のパターンを組んでおいた方が良いと感じます。<br />何かしら手詰まりに陥った状況では情報が少しでも多いのは助かりますし、もしかしたらこれが役に立つ場面があるかもしれません、くらいの認識です。

## 参考情報

Manipulating the browser history &#8211; MDN Docs  
<https://developer.mozilla.org/en/DOM/Manipulating_the_browser_history>

history.pushState、history.replaceState &#8211; 素人がプログラミングを勉強するブログ  
<http://d.hatena.ne.jp/javascripter/20100404/1270411268>
