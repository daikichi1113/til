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

## Laravelルートディレクトリのファイル構成
主なディレクトリ構成を解説する．次項で挙げる，よく使用するディレクトリを押さえれば当面はOK．

### app
アプリケーションのコアコードを配置する．
ModelやControllerもここに配置．
良く使用する．

### bootstrap
フレームワークの初期起動やオートローディングなどの設定ファイルが含まれる．
cache関連のファイルもここに保存される．
自分でファイルを作成する頻度は少なめ．

### config
アプリケーションの設定ファイルが保存される．

### database
データベースのマイグレーションファイルが保存される．
コマンドを実行した結果，生成されたファイルを編集する場合が多い．

### public
クライアントサイドのasset（css, javascriptなど）を配置する．
ここがドキュメントルートとなる．

### resources
Viewのファイルが保存される．
ブラウザで実際に表示させたい画面を作成するイメージ．

### routes
ルーティングを行うファイルを配置する．
ファイル自体ははじめから用意されているので，必要な処理に応じて追記する．

### tests
自動テストを配置する．

### vendor
composerでインストールしたパッケージが配置される．

## よく使用するディレクトリ&ファイル

### /.env
環境設定に使用

### /routes/web.php
ルーティングに使用

### /resources/views/***
Viewで使用するファイルを設定，保存

### /app/Http/controller/***
Model, Controllerを設定，保存

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

### カラム名の追記は「$table->カラム型('カラム名');」のように行う．
$table->increments('id');       //自動採番（主キー）
$table->string('email');        //varcharカラム
$table->string('name', 100);    //長さ指定カラム
$table->integer('price');       //integerカラム
$table->text('description');    //textカラム
$table->dateTime('created_at'); //datetimeカラム
$table->timestamps();           //created_atとupdated_atカラムを追加
$table->boolean('confirmed');   //true, falseカラム
$table->json('meta');           //jsonカラム

### カラムのオプションは以下の通り．
$table->string('email')->nullable();    //nullを許可
$table->string('email')->unique();      //カラムの値を一意にする

## 実行
php artisan migrate

### よく使うマイグレーションコマンドまとめ
マイグレーション実行．
$ php artisan migrate

直前に実行したマイグレーションをロールバックする．
$ php artisan migrate:rollback

全てロールバックしてからマイグレーションを再度実行する．
$ php artisan migrate:refresh

全てのテーブルを削除して再度マイグレーションを実行する．
$ php artisan migrate:fresh

マイグレーション状況を出力する．
$ php artisan migrate:status

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


# モデル
## model作成
php artisan make:model モデル名（頭文字は大文字）
※オプションで-mをつけると対応するマイグレーションファイルも自動生成される

例）php artisan make:model Task -m

# ルーティング
## ルーティングファイル
web.php　Laravelで通常のブラウザからのHTTPリクエストに対するルーティング設定を行う場合（WEB）
api.php　API通信などをルーティングする

## ルート定義メソッド
Route::resource('テーブル名', 'コントローラ名');
上記の一行は以下の処理をまとめたもの

例）Route::resource('tasks', 'TasksController');

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

# コントローラ
リクエストが来た際に，実際に実行される関数を定める役割を持つ．「どのリクエストに対してどの関数を実行するのか」はルーティングで定める．

コントローラは実行したい処理を関数として定義する．それぞれの関数内で，モデル（db関連の処理を実行）などに指示を出す．

コントローラのファイルは/project01/app/Http/Controllers以下に配置されるが，初期状態では作成されていない．

## コントローラの作成
php artisan make:controller コントローラ名（TasksController） --resource

オプションに--resourceをつけることで対応するよく使用するアクションもコントローラ同時に作成される（オプションを付与しない場合は自分で設定する必要あり）

以下２行は追記する
use Validator;　入力チェックを行う
use App\モデル名;　モデルを扱う

# View
## bladeテンプレート
Laravelのテンプレートエンジン。ビューの中にPHPを直接記述できる、つまりデータベースからのデータ表示などを簡単に記述する事ができる機能。

拡張子　.blade.php

bladeテンプレートは「ヘッダー」「フッター」「メニュー」などをパーツ化して共有利用できる．共有利用することで，編集するとどのページでも同時に更新することができる．
webページでは上記のパーツはどのページでも共通して用いられることが多いため，テンプレートエンジンを使用することで効率的に開発を進めることができる．
コントローラから渡された変数を{{ $test }}のように記述することで展開することができる．
また，テンプレート内でifを用いた条件分岐やforを用いた繰り返し処理を行うこともできる．
テンプレートを用いてビュー表示を行う際には，ファイル名に「*.blade.php」の拡張子をつける．
Laravelのビューは全て「resources/views」配下に設置する．

https://readouble.com/laravel/7.x/ja/blade.html

## 解説
@extends('layouts.app')は別ファイルの共通パーツ（ヘッダーなど）を呼び出している
@section('content')から@endsectionの記述内容がapp.blade.phpのcontent部分に挿入される．

@csrf
クロスサイトリクエストフォージェリ（CSRF）とは，Webアプリケーションに存在する脆弱性，もしくはその脆弱性を利用した攻撃方法のこと．掲示板や問い合わせフォームなどを処理するWebアプリケーションが，本来拒否すべき他サイトからのリクエストを受信し処理してしまう．

出所：クロスサイトリクエストフォージェリ（CSRF） (TREND MICRO)
@csrfを記述することでこのような不正リクエストを防ぐことができる．そのため，formでデータを送信する場合にはform内に@csrfを記述することが推奨される．

## エラー表示画面の作成
一覧画面内で呼び出しているエラー画面を作成する．/project01/resources/viewsにcommonディレクトリを作成する．更にcommonディレクトリ内にerrors.blade.phpを作成

## コントローラとの紐付け


# データベース処理
## 登録処理
ルーティングではRoute Nameでテーブル名.storeが定義されており（4.4項参照），実行される関数はテーブル名Controller.phpのstore()関数となる．

例）
$task = new Task;
テーブルに紐付いたTaskモデルを呼び出している．$taskがtasksテーブルを表現している，と解釈するとイメージが湧きやすい．

$task->task = $request->task;
formから送信されてきた値は$requestに配列の形で入ってくる．そのため，$task->task = $request->task;部分は「tasksテーブルのtaskカラムにformのname=taskから送信されてきた値を設定する」の意味となる

$task->save();
設定した値をテーブルに保存

## 表示処理
### dbからのデータ取得　コントローラー
変数（$テーブル名） = モデル名->get()

例）
$tasks = Task::orderBy('deadline', 'asc')->get()
tasksテーブルに対してorderByで並び順を変更し，get()でデータを取得する．

### ビューへデータを渡す　コントローラー
return view('テーブル名', ['テーブル名' => 変数（$テーブル名）]

例）
return view('tasks', ['tasks' => $tasks]);
['tasks' => $tasks]部分で$tasksの値（dbから取得したデータが入っている）をtasksという名前でtasks.blade.php側へ渡している．ビューへデータを渡すことにより，実際の画面へデータを表示させることができる

### ビューに表示させる　ビュー
・コントローラが渡したtasksのデータ（dbから取得したもの）が$tasksに入っている.
・bladeテンプレートでは，変数の内容をもとに条件分岐（@if）や繰り返し（@foreach）を用いて表示を制御することができる．

（@if (count($tasks) > 0)）　$tasksにデータが1レコード以上入っている場合
（@foreach ($tasks as $task)）　データを一覧で表示する
$tasksにdbから取得した全レコードが入っており，$taskに1レコードずつ入れて表示させている．$task->taskではtasksテーブルのカラム名を指定しているイメージ．

## 削除処理
### ビュー
フォームタグのアクションをdestroy
<form action="{{ route('tasks.destroy',$task->id) }}" method="POST">
route('tasks.destroy',$task->id)でルーティングのtasks.destroyにテーブルの各レコードidの値を送信している．idを指定することで，どのレコードを削除するのかを指定する．

フォームの中に削除ボタン
<form action="{{ route('tasks.destroy',$task->id) }}" method="POST">
  @method('delete')
  @csrf
  <button type="submit" class="btn btn-danger">削除</button>
</form>

上記の@method('delete')について
ルーティングで削除の部分はDELETEメソッドで定義しているが，formからの送信ではGETとPOSTの2つしか扱えない．そのため，form内に@method('delete')を記述してDELETEメソッドを使用できるようにしている．

### コントローラ
送信先のtasks.destroyに紐付いたdestroy関数の内容を記述する．

public function destroy($id)
{
  $task = Task::find($id);
  $task->delete();
  return redirect()->route('tasks.index');
}

ビューファイルから送信されたidが$idに入る
find()関数にidの値を渡すことで，該当する1レコードを指定している．
その後，delete()関数でレコードの削除する処理を実行．
削除の処理が完了したら，redirect()関数で一覧画面へ移動している．

## 更新処理
### ビュー
更新ボタン
<td>
  <form action="{{ route('tasks.edit',$task->id) }}" method="GET">
    @csrf
    <button type="submit" class="btn btn-primary">更新</button>
  </form>
</td>

<form action="{{ route('tasks.edit',$task->id) }}" method="GET">
クリック時にtasks.editへリクエストが送られる．削除ボタンと同様に，リクエスト送信時にレコードのid値が送信される

### コントローラ
public function edit($id)
{
  $task = Task::find($id);
  return view('taskedit', ['task' => $task]);
}

edit()関数にidが送信されると，テーブルから該当するidのレコードが取得され，taskedit.blade.phpを表示する．taskedit.blade.phpには，該当するレコードの内容がtaskという名前で渡されている．

### 更新用のビューファイルを作成
【解説1 / データの表示】前項のedit()関数で取得したデータが$taskに入っている．$taskの中身を各input要素のvalueに展開している．
【解説2 / データの送信】input要素で編集した値は，saveボタンクリック時にroute('tasks.update',$task->id)に送信される．ルーティングでは，tasks.updateへのリクエスト時にコントローラのupdate()が実行されるよう定義されているので，次項で処理を追記する

### コントローラーのupdateアクションを追記
【解説】処理の流れは登録の処理に酷似している．$task = Task::find($id);部分でidを指定しているため，該当するレコードが更新される．一方，登録処理のようにidを指定せずに実行するとデータが新しく作成される

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







