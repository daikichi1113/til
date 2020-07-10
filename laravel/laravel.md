# 環境構築

# Laravelのデバッグ方法
## Debugbar
Laravel用のデバッグをサポートするツール
Debugbarのインストールコマンド　composer require barryvdh/laravel-debugbar

インストール後、.env ファイルの中でAPP_DEBUG=trueとなっていればデバッグモード有効に。

## ログ出力
フォームからどのような値が入力されているか、 データベースにどの様に保存されたか、 変数の値はどうなっているか、というログを残す。

ログを残したいファイル上でuse Log; と記載し、Logファサードを使える様にした後に、Log::debug(ログを残したい内容);と記入する。

ログはlaravel.logファイルに保存される。

techpit-match/storage/logs
└── laravel.log

## ヘルパー関数
1) dd　処理を中断し、変数の中身などを確認できる。dump and dieの略。

ex:
変数の中身を確認したい場合

$test = [a, b];
dd($test);

結果
array:2 [
    0=>a
    1=>b
]

2)dump
ddと同様の使い方。ただし、ddの場合はdd以降の処理を停止するのに対し、 dumpは処理を止めないで実行される

３） var_dump()


# プロジェクト作成
composer create-project laravel/laravel プロジェクト名

※WEB環境があるところで実行すること<br>
※ver6以降はappkeyが自動付与される

# ローカルWEBサーバー起動コマンド
php artisan serve

# データベース設定（mySQL）
https://qiita.com/hitochan/items/f5dc22ecbe24a350276a

## タイムゾーンの変更
app.phpファイルを編集
'timezone' => 'UTC',　を　'timezone' => 'Asia/Tokyo',　へ
'locale' => 'en',　を　'locale' => 'ja',　へ

## エラーメッセージの日本語化設定
/resources/langフォルダの中にjaフォルダを作成し、その中に4つのファイルを作成。
enフォルダのファイル名と同じなのでコピーしても可

中身を、
https://github.com/minoryorg/laravel-resources-lang-ja/blob/master/resources/lang/ja/auth.php
のコードに書き換える

また、validation.phpに以下を追記
'attributes' => [
    'name'=>'名前',
    'email'=>'メールアドレス',
    'password'=>'パスワード',
],


# マイグレーション
## マイグレーションファイルの作成
php artisan make:migration cleate_テーブル名_table

※場所はdatabaseディレクトリ→migrationsディレクトリの中。
Laravelではインストールした時点であらかじめ、
・ユーザー情報を保存するテーブル情報
・パスワードリセット用テーブル
の情報が生成されている

## 作成したマイグレーションファイルの修正
public function up()
    {
        Schema::create('books', function (Blueprint $table) {
            $table->id();
            $table->string('title');  //ここに追記
            $table->timestamps();
        });
    }

※$table->型('カラム名');

## 実行
php artisan migrate

### マイグレートを実行して、以下のエラー分が出た場合

1)SQLSTATE[42S01]: Base table or view already exists: 1050 Table 〇〇 already exists

マイグレートファイルがある、というエラーなので、ロールバックして再度実行。
php artisan migrate:rollback

2)Database (database/database.sqlite) does not exist. (SQL: PRAGMA foreign_keys = ON;)

.envファイル修正（DB_DATABASE=をコメントアウト）

DB_CONNECTION=sqlite
DB_HOST=127.0.0.1
DB_PORT=3306
#DB_DATABASE=database/database.sqlite
DB_USERNAME=root
DB_PASSWORD=

https://qiita.com/stone_programer/items/12817f6d804d400e403e


# Laravelの構成

## MVCパターン
M・・Model(モデル)
V・・View(ビュー)
C・・Controller(コントローラー)

流れ
１）リクエストを送る
２）ルーティングファイルが処理先を振り分ける
３）コントローラが処理実行
４）必要あればモデル経由でデータベースにアクセス
５）ビューを生成しレスポンスとしてクライアントに表示

## HTTPリクエスト
大きくGETとPOSTの2種類がある。

GET・・データを受け取る用。パラメータがURLに表示される(検索条件などはこっちを使う)
POST・・データを保存する用。パラメータがURLに表示されない(ユーザー情報登録などはこっちを使う)


# View
## bladeテンプレート
Laravelのテンプレートエンジン。ビューの中にPHPを直接記述できる、つまりデータベースからのデータ表示などを簡単に記述する事ができる機能。

拡張子　.blade.php
ディレクトリ　通常はresources/viewsディレクトリに設置

https://readouble.com/laravel/7.x/ja/blade.html

## Laravel/ui Bootstrapの導入
### Laravel/ui のインストール
composer require laravel/ui

## フロントエンドのスカフォールドをインストール
// 基本的なスカフォールドを生成
php artisan ui bootstrap
php artisan ui vue
php artisan ui react

// ログイン／ユーザー登録スカフォールドを生成
・ユーザー登録機能
・ログイン機能
・パスワードリセット機能
・ログイン情報保存機能
・バリデーション(入力の有無、メールアドレスかどうかの判定)
がまとめて追加されている状態になる

php artisan ui bootstrap --auth
php artisan ui vue --auth
php artisan ui react --auth

## npm install
npm install

npm installを実施するタイミングでnode_modulesフォルダが生成
ッケージが更新されたりする場合にデータが上書きされてしまいますので、なるべくnode_modulesフォルダ内のファイルには手を入れない

## Font awesomeの追記
resources/sass/app.scssファイルを編集

/* Fonts */
@import url('https://fonts.googleapis.com/css?family=Nunito');

/* Variables */
@import 'variables';

$fa-font-path: "../webfonts"; /* 追記 */

/* Bootstrap */
@import '~bootstrap/scss/bootstrap';

@import "~@fortawesome/fontawesome-free/scss/fontawesome"; /* 追記 */
@import '~@fortawesome/fontawesome-free/scss/solid'; /* 追記 */
@import '~@fortawesome/fontawesome-free/scss/regular'; /* 追記 */
@import '~@fortawesome/fontawesome-free/scss/brands'; /* 追記 */

## ビルドコマンド
npm run dev

npm run dev ・・開発用にビルド
npm run watch ・・常時ビルド
npm run prod ・・本番用にビルド

# ルーティング
## ルーティングファイル
web.php　Laravelで通常のブラウザからのHTTPリクエストに対するルーティング設定を行う場合（WEB）
api.php　API通信などをルーティングする

## ルート定義メソッド
+------------+---------------------+----------+----------------+---------------------------+
| method     | uri                 | action   | route name     | explanation               |
+------------+---------------------+----------+----------------+---------------------------+
| GET        | /tasks              | index    | tasks.index    | データの一覧を取得する処理    |
| GET        | /tasks/create       | create   | tasks.create   | データ追加画面へ移動する処理   |
| POST       | /tasks              | store    | tasks.store    | dbへデータを追加する処理      |
| GET        | /tasks/{task}       | show     | tasks.show     | データを1件取得する処理       |
| GET        | /tasks/{task}/edit  | edit     | tasks.edit     | データ更新画面へ移動する処理   |
| PUT/PATCH  | /tasks/{task}       | update   | tasks.update   | dbのデータを更新する処理      |
| DELETE     | /tasks/{task}       | destroy  | tasks.destroy  | dbのデータを削除する処理      |
+------------+---------------------+----------+----------------+---------------------------+

# モデル
## model作成
php artisan make:model 単数形のテーブル名（頭文字は大文字）

例）php artisan make:model Book







## If文

@if (count($records) === 1)
    １レコードある！
@elseif (count($records) > 1)
    複数レコードある！
@else
    レコードがない！
@endif

## @unlessディレクティブ
@unless (Auth::check())
    あなたはログインしていません。
@endunless

## 認証ディレクティブ
@authと@guestディレクティブは、現在のユーザーが認証されているか、もしくはゲストであるかを簡単に判定するために使用します。

@auth
    // ユーザーは認証済み
@endauth

@guest
    // ユーザーは認証されていない
@endguest


必要であれば、@authと@guestディレクティブ使用時に、確認すべき認証ガードを指定できます。

@auth('admin')
    // ユーザーは認証済み
@endauth

@guest('admin')
    // ユーザーは認証されていない
@endguest


# route
## 基本的なルーティング
一番基本のLaravelルートはURIと「クロージャ」により定義され、単純で記述しやすいルートの定義方法を提供しています。

Route::get('パス', function () {
    return 'Hello World';
});

## ディレクトリ
routeディレクトリに４つのphpファイルが存在、WEBアプリの場合はweb.phpなど使い分ける

# ログイン認証
１）laravel/uiパッケージのインストール
composer require laravel/ui

２）ログイン／ユーザー登録スカフォールドを生成
<!-- php artisan ui bootstrap --auth -->
php artisan ui vue --auth
<!-- php artisan ui react --auth -->

Please run "npm install && npm run dev" to compile your fresh scaffolding. // コマンドラインに表示される

３）スタイルシートが壊れた場合は、npmから不足するパッケージをインストールすることで修復
npm install と npm run dev　の実行

結果：layoutsディレクトリにapp.blade.phpが自動で追加
　　　authディレクトリとその中身が自動生成
　　　App\Http\Middlewareにauth
     viewディレクトリにhome.blade.php追加　※ログイン成功画面

# ミドルウェア
プリケーションへ送信されたHTTPリクエストをフィルタリングする、便利なメカニズム。
例えばユーザー認証、CSRF保護など
app/Http/Middlewareディレクトリに設置される







