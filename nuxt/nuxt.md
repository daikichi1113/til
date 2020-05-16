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
.nuxtフォルダの中で確認できる

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
