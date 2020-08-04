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

dataが配列の場合、要素を取り出す時は{{ dataで定義した値[インデックス番号].要素のキー }}とかく
例） {{ items[0].name }}

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
汎用的なテキストフォーマット処理を適用する仕組み。
日付処理、パーセンテージ処理、数値を３桁毎にカンマを入れる処理などがあげられる

filters: {
  フィルタ名: function(value) {
    return ...
  }
}

テキストコンテンツでは、定義したフィルターは{{ 値|フィルタ名 }}として使う

例）
<div id="app">
    {{ item[0].price | numberWithDelimiter }}
  </div>

  <script>
  var item = [
  {
    name: "本",
    price: 1300,
    quantity: 0
  }]

  var vm = new Vue ({
    el: '#app',
    data: {
      item: item
    },
    filters: {
      numberWithDelimiter: function(value) {
        if (!value) {
          return 0
        }
        return value.toString().replace(/(\d)(?=(\d{3})+$)/g, '$1,')
        // 3桁毎にカンマを入れる
      }
    }
  })

  </script>

## 算出プロパティ（computed）
あるデータから派生するデータをプロパティとして公開する仕組み。
データそのものに何らかの処理を与えたものをプロパティにしたいときに用いる。

new Vue ({
  computed: { //関数として実装、参照時はプロパティとして機能
    算出プロパティ名: function(){
      // retuen ...
    }
  }
})

### thisによる参照
computedやmethodsで、dataや他の算出プロパティ（computed）を参照したいときは　this経由。

この[this]はVueインスタンス自身を指す。
※同一のcomputed/methods内やテキストコンテンツ内では使わないので混同しないこと。

## ディレクティブ
Vue.js独自の属性で、属性値の式の変化に応じたDOM操作を行う。
属性名は「v-」から始まる。

なお、Vueインスタンスをマウントした要素とその子孫でしか使うことができない。

<主なディレクティブ>
・v-if/v-show
・v-bind
・v-for
・v-on


### 条件付きレンダリング（v-if/v-show）
v-if/v-show：テンプレートの中の要素の表示・非表示を切り替える。
             いずれもtureで表示、falseで非表示。

例）
<div v-if="引数">
  // tureで表示、falseで非表示
</div>

<div v-show="引数">
  // tureで表示、falseで非表示
</div>

※v-ifとv-showの違い
・v-if：式の結果に応じてDOM要素を追加・削除する
・v-show：スタイルのdisplayプロパティの値を変更する

使い分けの基準は「切り替えの頻度」と「初期表示のコスト」。
・v-if：式の評価結果が変わらない場合に使用
・v-show：式の評価結果が変わる場合に使用
（レンダリングコストは、DOM操作＞スタイル操作のため）

### バインディング(v-bind)
v-bindは特殊な記法／　v-bind:属性名="データを展開した属性値"。

なお、属性名にclassまたはstyleを指定することでそれぞれのディレクティブが可能。
属性値にオブジェクトや配列を指定→要素やプロパティを結合→最終的に文字列として評価。

---【クラスのバインディング】
v-bind:class="オブジェクトまたは配列"  // 値が真のプロパティを属性値として反映。

属性値に入るオブジェクトはプロパティの数や値の式が複雑になると、templateのメンテナンスが大変になる。
そのため、オブジェクトをtemplateに調節記述するのではなく、算出プロパティとしてVueインスタンスに記述する方が良い。

---【スタイルのバインディング】
v-bind:style="オブジェクトまたは配列"  
  // 属性値のオブジェクトのプロパティがスタイルのプロパティと対応してインラインスタイルとして対応。

式と組み合わせて使うことも可能

属性値に入るオブジェクトはプロパティの数や値の式が複雑になると、templateのメンテナンスが大変になる。
そのため、オブジェクトをtemplateに調節記述するのではなく、算出プロパティとしてVueインスタンスに記述する方が良い。

### v-bindの省略記法
例） v-bind:disabled → :disabled


## リスト(繰り返し)レンダリング
v-forディレクティブ／オブジェクトや配列データを繰り返しレンダリングする

v-for='要素 in 配列'
v-for='値 in オブジェクト'
v-for='(値, キー) in オブジェクト'

補足：v-bind:key='~'で生成時に一意的なキーを各要素に与える

例）
<div id="app">
  <ul>
    <li v-for="item in items" v-bind:key="item.name">
      {{item.name}}: {{item.price}}×{{items.quantity}} = {{ item.price * items.quantity | numberWithDelimiter }}円
    </li>
  </ul>
</div>


## イベントハンドリング(v-on)
イベントが起きたときに属性値の式を実行する。jsのchangeやinputなどにあたる
v-on:イベント名="式として実行したい属性値"

例）
<div id="app">
    <p>{{ number }}回クリックされています</p>
    <button v-on:click="countUp">カウントアップ</button>
    <p v-on:mousemove="changeMousePosition">マウスを乗せてください</p>
    <p>X：{{x}} Y：{{y}}</p>
  </div>

  <script>
    new Vue ({
      el: "#app",
      data: {
        number: 0,
        x: 0,
        y: 0
      },
      methods: {
        countUp: function() {
          this.number += 1
        },
        changeMousePosition: function(event) {
          this.x = event.clientX
          this.y = event.clientY
        }
      }
    });
  </script>

※eventオブジェクトを引数にとるときは$eventと表記する

https://jp.vuejs.org/v2/guide/events.html
https://developer.mozilla.org/ja/docs/Web/Events

### v-onの省略記法
v-on:click → @click


## フォーム入力バインディング（v-model）
フォーム入力のバインディング

<input type="number" v-model="item.quantity" min="0">

## ライフサイクルフック

## メソッド(methods)
Vueインスタンスのメソッドとして機能し、データの変更やサーバーにHTTPリクエストを送る際に用いる。
Vueインストラクタオプションのmethodsプロパティで定義する。

<button v-on:click="doBuy"></button>



例）インストラクタの書き方
methods: {
  メソッド名: {
    // 処理
  }
}

例）templateでの呼び出し方
{{ メソッド名() }}

### イベントオブジェクト
v-onディレクティブの属性値にメソッドを指定した場合、引数にはデフォルトでイベントオブジェクトが渡される

このオブジェクトには、イベントが発生した要素や座標などの情報が含まれる。

例）
methods: {
  メソッド名: function(event) {  //引数eventはイベントオブジェクト
    // 処理
  }
}

## conputedとmethodsの違い
computed：リアクティブな依存関係が更新されたときにだけ再評価される。
methods：再描画が起きると常に関数を実行する。

つまり、methodsは描画元に関係ない値が変更された時でも関数を実行している。
なので、計算する関数はcomputedを使った方が良い（計算処理が重くなる）

https://jp.vuejs.org/v2/guide/computed.html

# コンポーネント
