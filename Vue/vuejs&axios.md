vue.jsを使ってaxiosを学ぶ

# axiosの使用方法
## axiosとは
PromiseベースのHTTP ClientライブラリでGETやPOSTのHTTPリクエストを使ってサーバからデータの取得、サーバのデータの更新を行うことができる

## javascrptのpromiseとは
非同期の処理をいい感じに使えるAPIパターン。
Promiseが2つの結果を持ちどちらかの一方の結果を戻す。
pending、resolved, rejectedの3つのステータスを持っている。

https://reffect.co.jp/html/promise-is-what

＜promiseのメソッド＞
呼び出した関数の戻り値。呼び出すことで値を受け取れるため、実装した関数を使う場合に使用する。
.then Promiseの処理がresolveされた場合に呼び出される関数
.catch Promiseの処理がrejectされた場合に呼び出される関数
※.thenメソッドの第二引数もrejectされた場合に呼び出される関数となる

https://qiita.com/koki_cheese/items/c559da338a3d307c9d88

## GETメソッド
引数からデータを取得してくる。リクエスト後に戻される値はすべてresponseの中に保存される。

function() {
  axios.get(引数)
    .then  //データを取得できた場合
    .catch //データを取得できなかった場合

流れとしては、
・getメソッドでデータの取得
・thenメソッドでresponse.dataをVueのdataに保存する
・vueのディレクティブでブラウザに表示させる

例）
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
</head>

<body>
  <div id="app">
    <ul>
      <li v-for="user in users">{{ user.name }}</li>
    </ul>  
  </div>

<script>
new Vue({
  el: '#app',  //scriptが有効なid
  data: {
    users: []  //取得先の場所（ここでは配列）を用意する
  },
  mounted :function(){
    axios.get('https://jsonplaceholder.typicode.com/users')
          .then(response => this.users = response.data)
          .catch(response => console.log(response))
  }
})
</script> 
</body>
</html>

## GETメソッドにフィルターをかける
パラメーターをつける または パラメータオプションを使う


## POSTメソッドによる新規作成
新規にデータを登録する。POSTの場合はGETとは違いデータを作成するのに必要な項目と値の組を設定する必要がある。

axios.post('/data', {
  data1: 'data1'
  data2: 'data2'
})
 .then
 .catch

第一引数（data）に第二引数（data1,data2）を登録する

例）
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
</head>

<body>
  <div id="app">
    <input v-model="name"><br> 
      //追加する先をinputとv-modelで指定
    <button v-on:click="createNewUser">作成</button> 
      //作成ボタン。clickイベントでcreateNewUserメソッド発火
    <ul>
      <li v-for="user in users">{{ user.name }}</li>
    </ul>
    </div>

<script>
new Vue({
  el: '#app',
  data: {
    users: [],
    name:''    //postで登録するdataの場所(DBならカラム)
  },
  methods :{  //methodsプロパティ
    createNewUser: function(){  //メソッド名: function()実行する関数
      axios.post('https://jsonplaceholder.typicode.com/users', {
            name: this.name
           })
          .then(response => this.users.unshift(response.data)) //data配列の先頭に追加
          .catch(response => console.log(response))     
    }
  },
  mounted :function(){
    axios.get('https://jsonplaceholder.typicode.com/users')
          .then(response => this.users = response.data)
          .catch(response => console.log(response))
  }
})
</script> 
</body>
</html>


## DELETEメソッドによるデータの削除
データの削除。DELETEするデータを識別するIDが必要となる。

axios.delete('/data/id')
 .then
 .catch

例）
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
</head>

<body>
  <div id="app">
    <input v-model="name"><br>
    <button v-on:click="createNewUser">作成</button>
    <ul>
      <li v-for="user in users">{{ user.name }}:<button v-on:click="deleteUser(user.id)">削除</button></li>
      // リストの横に削除ボタン
      // 識別するためにdeleteUserの引数にid(ここではuser.id)を設定
    </ul>
    </div>


<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

<script>
new Vue({
  el: '#app',
  data: {
    users: [],
    name:''
  },
  methods :{
    createNewUser: function(){
      axios.post('https://jsonplaceholder.typicode.com/users', {
            name: this.name
           })
          .then(response => this.users.unshift(response.data))
          .catch(response => console.log(response))     
    },
    deleteUser: function(id){
      axios.delete('https://jsonplaceholder.typicode.com/users/' + id)
          .then(response => console.log(response))
          .catch(response => console.log(response)) 
    },
  },
  mounted :function(){
    axios.get('https://jsonplaceholder.typicode.com/users')
          .then(response => this.users = response.data)
          .catch(response => console.log(response))
  }
})
</script> 
</body>
</html>

## PUTメソッドによるユーザの更新
axiosのPATCHメソッドを利用して、データを更新する
PATCHでは既存のデータの上書きを行うので、更新したい項目と値の組を指定する必要がある。
また、更新するユーザを識別するIDも必須。

axios.patch('/data/id',{
   data1: 'data1',
   data2: 'data2'
  })
  .then
  .catch

更新の場合はvue.js側の設定が少し複雑になり、axiosの動作確認からは離れてしまうことも考えられるので注意

## エラーについて