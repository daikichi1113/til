# scriptタグについて
scriptタグはhtmlのbodyタグの中でもOK.複数あっても良い。
jsファイルなど別のファイルに記載するときはhtmlで読み込む必要がある。
jsファイルにはscriptタグ不要

## htmlの直接ブラウザ表示
HTMLファイルはブラウザにドラックすることで表示できる。
フレームワークが必要ない場合などに使用。

# console.log
scriptタグのデバッグでconsole.logを使う場合、検証ツールのコンソールを活用。

※コンソール上でのconsole.log()はページ表示時の値となるため注意。
※関数の戻り値などの数値は、関数内にconsole.log()を記載し、イベント発火をさせてコンソールに表示させる

# イベントハンドラ
イベント＝マウスボタンをクリックした、ページが読み込まれたなどの動作が起こった時に発生する

イベントハンドラ＝イベントを検出し、発生したイベントごとに処理を実行することができる。

イベントハンドラはそれぞれで指定できる要素が異なる。

## イベントハンドラ一覧
https://phpjavascriptroom.com/?t=js&p=event

# this
別のfunctionの関数を使うときは、this.関数()

# document.getElementBy

## .textContent

## .value

# 切り捨て・切り上げ・四捨五入
// 切り捨て
var a = Math.floor( 1.5 ) ;

// 切り上げ
var b = Math.ceil( 1.5 ) ;

// 四捨五入
var c = Math.round( 1.5 ) ;

# スコープ
関数A内で定義した変数Aを他の関数Bで使う場合

関数Aの返り値として変数Aをreturn。
関数B内でthis.関数Aとする

# 文字列を数値に
Number(変数)

# jQueryでselectタグの値やテキストを取得する
https://www.flatflag.nir87.com/select-2-1240

# 動的なセレクトボックス
https://techacademy.jp/magazine/27133
https://javascript.programmer-reference.com/js-select-prefecture/
https://javascript.programmer-reference.com/js-selectbox-linkage/

# appendChildメソッド
https://techacademy.jp/magazine/20820

# イベントドリブンプログラミング
イベントハンドラ・・・1つの要素、イベントについて１つしか設定できない
イベントリスナ・・・1つの要素に複数イベントを設定することができる。

対象要素.addEventListener(種類, sampleEvent, false);

function sampleEvent() {
  //ここに処理を記述する
}

https://qiita.com/makoto1219/items/0ce5463da09d6c1a44a5
https://techacademy.jp/magazine/20950
https://www.sejuku.net/blog/57625

# イベントリスナー内のthis
イベントリスナーで呼ばれる関数内のthisは、メソッドのthisになるため、そのメソッドが属するオブジェクトを指す。
そのため、先にthisを退避させ、確保しておく。

例
var _this = this

詳しくは↓
http://enlosph.hatenablog.com/entry/2017/01/20/222605

# 何もしない
 ;

https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/Empty

# 数値かどうか
typeof

https://www.javadrive.jp/javascript/ope/index15.html
https://zero-plus-one.jp/javascript/isnumber/

# 数値を通貨に変更
toLocaleStringメソッド
https://hacknote.jp/archives/27156/

# ページ遷移の値渡し
https://phpjavascriptroom.com/?t=js&p=location4

# ブラウザバック対策
https://sevenb.jp/wordpress/ura/2016/02/22/web%E6%88%BB%E3%82%8B%E3%83%9C%E3%82%BF%E3%83%B3%E3%81%A7%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E3%81%8C%E6%AE%8B%E3%81%A3%E3%81%A6%E3%81%84%E3%82%8B%E3%81%AE%E3%81%8C%E5%9B%B0%E3%82%8B%E5%A0%B4/

# div枠全体をリンクする方法
https://www.ipentec.com/document/html-css-link-entire-div-frame#section_09

<head>
    <meta charset="utf-8">
    <title>nagasaki-mc</title>
    <link rel="stylesheet" type="text/css" href="reset.css">
    <link rel="stylesheet" type="text/css" href="index.css">
    <script type="text/javascript">
        function AboutFrameClick() {
          document.location.href = "https://nagasaki-mc.hosp.go.jp/about/about.html"
        }
    </script>
</head>

<body>
  <div onclick="AboutFrameClick()">
    <h2>病院のご案内</h2>
    <p>About</p>
  </div>
</body>

*aタグではないのでカーソルがポインタにならないので注意。cssで該当classに「cursor: pointer;」記述


