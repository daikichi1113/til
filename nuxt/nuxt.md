# 新規プロジェクトの作成１
## スクラッチ
### package.json
プロジェクトには、 nuxt を起動するために package.json ファイルが必要.
以下のコードを記述する
{
  "name": "my-app",
  "scripts": {
    "dev": "nuxt"
  }
}

### nuxt のインストール
package.json を作成したら nuxt を npm でプロジェクトに追加
$ npm install --save nuxt

### pages ディレクトリ
.vueファイル

### プロジェクト起動
npm run dev

# 新規プロジェクトの作成２
## npx利用
npx nuxt-create-app プロジェクト名
途中、質問がある。

## プロジェクト起動
npm run dev

# マスタッシュ（Mustache）構文
<p>{{ msg }}</p>
二重中括弧 {{}} を利用したテキスト展開
ただしHTML属性内部で使用することができない

<!-- 以下のようなことは不可 -->
<img src="{{ src }}">
<a href="{{ url }}"></a>

<!-- v-bind:attr="variable" という形で使う -->
<img v-bind:src="src">
<a v-bind:href="url"></a>

<!-- v-bind は省略可 -->
<img :src="src">
<a :href="url"></a>

# ルーティング(vue router)
nuxt.jsではルーティングの設定を自動で行っている
.nuxt/route.js　*.nuxtフォルダ(隠しフォルダ)の中

## vue router
vue router公式
https://router.vuejs.org/ja/

## path
index = /

pages
 - index.vue → /
 - users
   - index.vue → /users/
   - other.vue → /users/other

## バリデートメソッド
<script>
export default {
  deta: function() {
    return {
      message: '/user/_id.vueを表示中'
    }
  },
  validate({ params }) {
    return /^\d+$/.test(params.id)
  }
}
</script>

/^\d+$/.test(params.id)　数値のみtrue

\ は　option + ¥

# ビュー
## アプリテンプレートレイアウト
.nuxt/view/app.template.html *.nuxtフォルダ(隠しフォルダ)の中

※テンプレートレイアウト（app.template.html）をカスタマイズしたい場合
・app.template.htmlはいじらない
・プロジェクト直下に「app.html」ファイルを作成
・app.htmlにapp.template.htmlのコードをコピペして利用

## noscript
noscriptとは、scriptタグと一緒に使用し、scriptタグに対応していないブラウザへのメッセージを記述します。つまり、scriptタグに対応しているブラウザではnoscriptタグは無視され、対応していないブラウザではnoscriptタグの間の内容が表示されます。

<script type="text/javascript">
  document.write("スクリプトが実行された場合");
</script>
<noscript>
  <p>スクリプトが実行されない場合</p>
</noscript>

## デフォルトレイアウト
ページの基本的なレイアウトを定義する

### layouts/default.vue
default.vue　レイアウトが明示的に指定されていない全てのページに使用される

<template> ※コンポーネントの基本となるプロパティ
  <div>
    <nuxt />　※nuxtコンポーネント　各ページで異なるページコンポーネント
  </div>
</template>

<style>　※各ページで共通するスタイルは「default.vue」にかくとよい

</style>


### 関係性
app.html　＊htmlの大枠を記述
:
layouts/default.vue　＊デフォルトのレイアウト、サイト共通のスタイルなど
:
pages/index.vue など

●app.html
<html {{ HTML_ATTRS }}>
  <head {{ HEAD_ATTRS }}>
    {{ HEAD }}
  </head>
  <body {{ BODY_ATTRS }}>
    <noscript>Your browser does not supprt Javascript!</noscript>
    {{ APP }}　◀︎　layouts/default.vue　が表示
  </body>
</html>

●layouts/default.vue
<template>
  <div>
    <nuxt />　◀︎　pages/index.vueなど　が各ページで異なるコンポーネント表示
  </div>
</template>

## エラーページのカスタマイズ
/layoutsにerror.vueを作成

例

<template>
  <div>
    <h1 v-if="error.statusCode === 404">error! 404</h1>
  </div>
</template>

<script>
  export default {
    props: ['error']
  }
</script>j

＊error.vueには<nuxt />は含んではいけない

### props(コンポーネントに自由にデータを渡す)
親から子に自由にデータを渡せるもの

### フロントエンドの描画を条件分岐(表示／非表示)
●v-if, v-else-if, v-else
v-if="条件"と書くことで条件の真偽によりその要素を表示するかしないかをコントロール


## HTMLヘッダーのカスタマイズ
.nuxt.config.js の　headタグをカスタマイズ

linkタグは配列になっている


# 非同期データ通信
## axios
axiosとはブラウザやnode.js上で動くPromiseベースのHTTPクライアント。非同期にHTTP通信を行いたいときに容易に実装できる.
javascriptの一般的なライブラリ
Vue.js（nuxt.js）では非同期通信を行うのにaxiosを使うことが推奨されている

インストールコマンド　npm install axios　＊プロジェクトディレクトリで実行

*インストールされているパッケージ情報を確認するときはpackage.jsonを参照

### Promiseと.then()
非同期処理の結果を、成功（resolve） または、失敗（reject）で返すオブジェクト。以下のような非同期処理を簡潔に書ける。

・非同期処理の成功、失敗の処理を分岐する。
・複数の非同期処理を順番に実行したり、並行して実行する。（直列・並列）

then() メソッドは Promise を返す。最大2つの引数、 Promise が成功した場合と失敗した場合のコールバック関数を取る。

## データを取得
<template>
  <div class="container">
    {{ users }}
  </div>
</template>

<script>
const axios = require('axios')
let url = 'https://jsonplaceholder.typicode.com/users'

export default {
  asyncData({ params }) {
    return axios.get(url)
      .then((res) => {
        return { users: res.data }
      })
  }
}
</script>

＊asyncDataメソッド／Nuxt.jsのメソッド。コンポーネントを初期化する前に非同期の処理を行うようにする。

＊axios.get(url)／APIからのデータ取得をリクエスト。レスポンスを受け取った段階で.thenメソッドが呼ばれる。

＊(res)／サーバーからのレスポンスデータが入っている

＊res.data／jsonオブジェクトが入っている。サーバーから取得したjsonテキストをaxiosがjavascriptオブジェクトに変換している

＊{ users: res.data }　／　res.dataにusersという名前をつける

### １つのデータを取得
<template>
  <div class="container">
    {{ users[0].id }}, {{ users[0].name }}
  </div>
</template>

※データを取り出すにはインデックスを指定する

### 複数データを取得(リストレンダリング（v-for 配列の繰り返し）)
<template>
  <div class="container">
    <ul>
      <li v-for="user in users" :key= user.id >
        {{ user.id }}, {{ user.name }}
      </li>
    </ul>
  </div>
</template>

＊　リストレンダリング（v-for 配列の繰り返し）
v-for="変数 in 配列" :key="変数.id"

## エラーハンドリングの実装
export default {
  asyncData({ params, error }) {
    return axios.get(url)
      .then((res) => {
        return { users: res.data }
      })
      .catch((e => {
        error({ users: e.response.status, message: e.message })
      }))
  }
}

.catchメソッド　

e 　変数（エラー情報が入っている）

エラーメソッド（エラーページを表示する）
error({ users: e.response.status, message: e.message })

e.response.status　ステータスコード


# アセット
## 画像の表示
assetsディレクトリに保存して呼び出す　~/assets/ファイル名

## 静的なファイルの公開
favicon.ico、robots.txt、sitemap.xmlなど<br>
静的なファイルを公開するにはstaticディレクトリ内にファイルを作成する<br>
ホームディレクトリ/ファイル名で表示できる

# Vuex
Vue.jpのために開発されたアプリケーションの状態(state)管理を行うライブラリ。複数のコンポーネントで使える値などをストアと呼ばれる保管場所でまとめて管理する。

１つのアプリケーションが持つストアは１つ。
各コンポーネントからstateを直接操作することはルール違反。ミューテーションを経由する


## 2つのモジュールモード
クラシックモード（ベーシック）<br>
モジュールモード（大規模開発）

## Vuex とは何か？
https://vuex.vuejs.org/ja/

## データフロー
コンポーネント
: （リクエスト）
アクション ◀︎　▶︎　外部API
:
ミューテーション
:
ステート
:
コンポーネント

*ステート(state) アプリケーションの状態を保持.ストア

*アクション(actions) 外部APIとの通信を行い、ミューテーションを呼び出す。外部APIとの非同期処理が必要なときはここに置く。

*ミューテーション(Muttions) Vuexのストアの状態を唯一変更できる

## ストアの作成
storeディレクトリにindex.jsを作成する

import Vuex from 'vuex' *Vuexのインポート

const createStore = () => { *ストア作成はアロー関数を用いる
  return new Vuex.Store({
    state: function() { *stateの値は常にfunctionにする
      return {　*使用する値をオブジェクトにして返す
        message: 'Hello Vuex' 
      }
    }
  })
}

export default createStore　＊エクスポート


### アロー関数
ES6から導入された新しい書き方
function()
↓
()=>

### ストア情報の表示
例　<p>{{ $store.state.message }}</p>
Vuex.Storeのstateで用意したmessageの値を呼び出す

## ミューテーションの利用（ストアの値をコンポーネント側から変更）
https://vuex.vuejs.org/ja/guide/mutations.html

stateの値を変更する場合
ストア側　値の操作を行う処理を用意
コンポーネント側　上記の処理を呼び出す

index.js(ストア側)
const createStore = () => {
  return new Vuex.Store({
    state: function() {
      return {
        message: 'Hello Vuex'
      }
    },
    mutations: {
      updateMessage: function(state) {
        state.message = 'Updated!'
      }
    }
  })
}

index.vue(コンポーネント側)
<template>
  <div class="container">
    <div>
      <p>{{ $store.state.message }}</p>
      <button v-on:click="$store.commit('updateMessage')">Update</button>
    </div>
  </div>
</template>

１）コンポーネント側でボタンをおしてストアのupdateMessageミューテーションを呼び出す
２）updateMessageの処理を行いstate.massageを上書きする

＊<button>タグは、ボタンを作成する際に使用
＊v-on
＊commitメソッド/ミューテーションのタイプを指定して store.commit を呼び出す

### イベントハンドリング
v-onディレクティブ
DOM イベントの購読、イベント発火時の JavaScript の実行が可能になる。

例）
<button v-on:click="counter += 1">Add 1</button>

## ミューテーションの値渡し
コミットメソッドの第二引数に渡したい値を入れて、ミューテーションがわの第二引数で値を受け取る

index.vue
<button v-on:click="$store.commit('updateMessage', 'commit with payload')">Update</button>

index.js
mutations: {
  updateMessage: function(state, payload) {
    state.message = payload
  }
}

### payload


## アクションの利用
アクションはミューテーションと似ているが、下記の点で異なる

・状態を変更するのではなく、context.commit を呼び出すことでミューテーションをコミットする。
・任意の非同期処理を含むことができる

また、アクションは store.dispatch がトリガーとなって実行される


例）
●index.jsでactionsを設定
},
actions: {
  アクション名(context) {
    context.commit('ミューテーション名', 'commit with payload')
  }
}

●index.vueで実行
<button v-on:click="$store.dispatch('アクション名')">dispatch</button>

## アクションに値を渡す
index.vue
例）
<button v-on:click="$store.dispatch('updateMessageAction', 'dispatch with payload')">dispatch</button>

dispatchメソッドの第２引数に値をいれる

index.js
例）
actions: {
  updateMessageAction(context, payload) {
    context.commit('updateMessage', payload)
  }
}

actionの第２引数にpayload
commitメソッドの第２引数にpayload

## モジュールモードの利用
複数のファイルに記述できる

クラシックモードからモジュールモードへの移行はストアの記述方法が変更となる

### モジュールモード動作の条件
・index.jsがストアオブジェクトをexportしない
または
・index.jsがstoreフォルダ配下に存在しない