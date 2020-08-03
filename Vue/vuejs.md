# vue.jsのでUIを構築するときの考え方
イベントとDOM要素の間にstate（UIの状態）が挟まる形となっている

event--------↓      |--------element
event------→ state -|--------element
event--------↑      |--------element

・event発火によるstate(uiの状態)変更
・state(uiの状態)変更に伴ったDOMの更新
と２つに分けて考えることができるため、イベントの要素やDOM要素が複雑（多い）場合に有効。

# Vueオブジェクト
## コンストラクタ
javascriptでオブジェクトを生成するための関数。コンストラクタとして使う場合はnew演算子を使う。

Vue new ({
  //
})

生成されたオブジェクトをVueインスタンスと呼ぶ。
インスタンスをDOM要素に適用することでVuejsの機能がその要素内で使え雨ようになる。

## オプションオブジェクト
コンストラクタの引数として渡す役割。指定できるものは以下の通り。

オプション名：内容
data   ：UIの状態・データ
el     ：Vueインスタンスを適用する要素
filters：データを文字列と整形する
method ：イベントが発生した時などの振る舞い
computed:データから派生して算出される値

## コンポーネント

## Vueインスタンスの適用（ei）
オプションオブジェクトのelプロパティで指定したDOM要素がマウント（適用）対象となる。
elプロパティにはDOM要素のオブジェクトかCSSセレクタの文字列を指定できる

例）
new Vue ({
      el: "#app"   ///id=appのdivをマウント対象として指定。
    });

## UIデータの定義（data）
dataプロパティ： UIの状態となるデータのオブジェクトを指定。マウント後の表示に欠かせない。

Vuejsの表示の基本的な仕組み
・Vueインスタンス生成時にdataを与えておき、それをテンプレートで表示する

例）
new Vue ({
      el: "#app",
      data: {
        message:"hello-world"  /// dataプロパティ。変数messageをhello-worldと定義する
      }
    });

## テンプレート構文
データ（Vueインスタンス）とビュー（DOMツリー）の関係を宣言的に定義する（データが決まればビューの内容が決定される）。

### マスタッチェ記法によるデータの展開
  テキストコンテンツ内でVueインスタンスのdataを展開する。{{}}を使う。
  マスタッチェ構文では{{}}の中でdatasで定義したデータの他、算出プロパティ、メソッド、フィルタも参照できる

  例）
<body>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <div id="app">
    <p>{{ message }}</p>   ///dataのmessageを表示する
  </div>
  <script>
    new Vue ({
      el: "#app",
      data: {
        message:"hello-world"
      }
    });
  </script>
</body>

### ディレクティブによるHTML要素の拡張
テキストコンテンツ内でDOMの属性に対して展開する。v-vindを使う。

v-vind・・・Vue.jsのディレクティブの１つ。v-vind:属性名="データを展開した属性値"で使う

例）
<body>
<div>
  <button id="b-button" v-vind:title="buyButton">購入</button>
</div>

<script>
  new Vue ({
    el:"b-button",
    data: {
      buyButton:"購入しますか？"
    }
  });
</script>
</body>

### javascript式の展開
javascript式で展開も可能。ただし、複雑化しがちなので用いるなら簡単なものにする

## フィルタ（filters）
汎用的なテキストフォーマット処理を適用する仕組み