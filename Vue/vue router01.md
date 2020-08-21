# Vue Routerとは

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
