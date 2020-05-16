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
## テンプレートレイアウト
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

# デフォルトレイアウト
ページの基本的なレイアウトを定義する

## layouts/default.vue
default.vue　レイアウトが明示的に指定されていない全てのページに使用される

<template> ※コンポーネントの基本となるプロパティ
  <div>
    <nuxt />　※nuxtコンポーネント　各ページで異なるページコンポーネント
  </div>
</template>

<style>　※各ページで共通するスタイルは「default.vue」にかくとよい

</style>


## 関係性
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
