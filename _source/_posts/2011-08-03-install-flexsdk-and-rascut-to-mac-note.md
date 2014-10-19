---
layout: post
title: macbook へ Flex SDK と rascut を入れる際に大変参考になった URL
---
詳しい導入手順はググれば色々出てくるので、  
自分が真似てみて実際に遭遇したエラーなんかのメモです。

1. Flex SDK は適当にググッて好きな場所へ配置  
(~/Library/Flex/flex_sdk_4.5.1/ にしときました。)
2. mxmlc が早速コンソールで文字化けを起こしたところ、こんな記事があって助かりました。

   Mac OS Xで、Flex SDK 4.5を使ってゲームを作るためにやったこと &#8211; teikouの日記  
   <http://d.hatena.ne.jp/teikou/20110702>

3. mxmlc Hello.as と、Hello World し終えたので rascut も入れようとするけどエラー。  
まさにこちらの記事の通りだったので、これもまた大助かりです。  
先に mongrel を &#8211;pre オプションで入れると良い模様。

   rascut + Ruby 1.9.2 &#8211; ikeasの日記  
   <http://d.hatena.ne.jp/ikeas/20110416/1302949899>

4. rascut を起動するともう一度エラー。これも上記の記事の後半の手順で対応できました。
5. これでコンソールから rascut Hello.as のコマンドで Hello.as の変更を監視。  
変更があったら自動でコンパイルをしてくれるようになりました。

