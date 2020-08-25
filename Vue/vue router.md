# はじめてのVue Router(基本編)

# Vue Routerの基本設定
## Vue Routerコンポーネント
router-link、router-viewコンポーネントを利用

router-linkタグはリンクを作成するために使用。
router-viewタグは、それぞれのリンク先に紐づいた内容を表示するために使用。

router-viewタグの中身はJavaScript側で制御されている

## ルーティングのためのscriptタグの中身
scriptタグの中では大きく3つのパートに分けて設定を行なっている

(1)コンポーネントの設定
   各コンポーネントのtemplateプロパティに表示させたいHTMLを記述

   例）
    const Home = { template: '<div>初めてのVue Resource</div>'}
    const News = { template: '<div>今週のニュースは....</div>'}
    const About = { template: '<div>会社までのアクセス方法は....</div>'}

(2)ルーティングの設定
   パスと表示させる内容を紐づける

   例）
   const router = new VueRouter({
      routes : [
        {path:'/', component : Home},
        {path:'/news',component: News},
        {path:'/about',component: About}
      ]
    })

(3)Vueインスタンスへrouterインスタンスを渡す

  例）
  var app = new Vue({
      el: '#app',
      data:{
        title: 'Vue Resource',
      },
      router,
    });


# Vue routerを活用したアプリケーション開発
Vue Router …vuejsの公式プラグイン。
            SPAをはじめとする"URL遷移を伴う動作"を簡単に実装できる。

## シングルページアプリケーション(SPA)とは
はじめに１つのHTMLをロードし、以後はユーザーインタラクションに応じてAjaxで情報を取得して動的にページを更新するWEBアプリのこと。

SPA実装の際に考慮すること
・クライアントサイドでの利益管理も含めたページ遷移
・非同期によるデータ取得
・Viewのレンダリング
・モジュール化されたコードの管理
→これらの機能を担うのがルーターやルーディングライブラリ。

## Vue Routerとは
SPA構築のためのルーディングライブラリ（公式プラグイン）。
宣言的にページ遷移のルールを定義し、アクションに応じてVuejsコンポーネントがアクティブになるという仕組みで動作する。

vue Routerの機能
・基本的なページ遷移
・ネストしたルーディング
・リダイレクトとエイリアス
・履歴管理
・自動的にCSSクラスがアクティブになるリンクの仕組み
・ページ遷移時のトランジション
・スクロールの振る舞いのカスタマイズ

## ルーディングの基礎
Vue Routerのインストール ...スクリプト要素で本体に続けて読み込む。
                          CDNサービスを使うと便利。
https://jp.vuejs.org/v2/guide/installation.html

### ルーディング設計
ルート…Vue RouterにおけるルートはVuejsのコンポーネントを特定のURLマッピングオブジェクト。
      これをルーターコンストラクタを用いたルーター初期化時のrouteオプションに設定する　。