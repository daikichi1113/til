# 変数の使い方
変数の定義　$変数名: 値;<br>
※変数は利用する箇所より前で定義する

# mixin
いくつかのコードを1つにまとめて、複数箇所で簡単に呼び出すことができる機能

## mixinの定義
@mixin mixin名 { コード }

## mixinの呼び出し
使用したいSassファイルの中で「@include mixin名;」とする

## mixinと引数
mixinには色などの情報を「引数（ひきすう）」として渡すことができる

# 関数
darken関数 color: darken(色, 割合);<br>
lighten関数 color: lighten(色, 割合);<br>
rgba関数 color: rgba(色, 透明度);

# import
外部のファイルを読み込む<br>
読み込み先のファイル名の先頭には「_（アンダーバー）」を付ける<br>
@import "ファイル名"; ※_（アンダーバー）」と拡張子（.scss）を省略できる