# laravelはcomposerで動く

# プロジェクト作成
composer create-project laravel/laravel プロジェクト名

※WEB環境があるところで実行すること<br>
※ver6以降はappkeyが自動付与される

# ローカルでWEBサーバー起動
php artisan serve

# マイグレーション
## マイグレーションファイルの作成
php artisan make:migration テーブル名_table

※場所はdatabaseディレクトリ→migrationsディレクトリの中。標準でusersのマイグレーションファイル、Userモデルが用意されている。

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

# データベース設定（sqlite）
.env → DB_CONNECTION=使用するDB名（デフォルトはmysql）
       DB_DATABASE=絶対パス

/config/database.php → 'default' => env('DB_CONNECTION', '使用するDB名（デフォルトはmysql),)

/databaseディレクトリの中にdatabase.sqliteファイルを作成
touch database.sqlite

# データベース設定（mySQL）
https://qiita.com/hitochan/items/f5dc22ecbe24a350276a

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


# モデル
## model作成
php artisan make:model 単数形のテーブル名（頭文字は大文字）

例）php artisan make:model Book


# Bladeテンプレート
BladeはシンプルながらパワフルなLaravelのテンプレートエンジン。ビューの中にPHPを直接記述できる。

※全BladeビューはPHPへコンパイルされ、変更があるまでキャッシュされます。つまりアプリケーションのオーバーヘッドは基本的に０です。Bladeビューには.blade.phpファイル拡張子を付け、通常はresources/viewsディレクトリの中に設置します。

## データ表示
Bladeビューに渡されたデータは、波括弧で変数を囲うことで表示できます。

例）
Route::get('greeting', function () {
    return view('welcome', ['name' => 'Samantha']);
});

Hello, {{ $name }}.

※　Bladeの{{ }}記法はXSS攻撃を防ぐため、自動的にPHPのhtmlspecialchars関数を通されます。

ビューに渡された変数の内容を表示するだけに限られません。PHP関数の結果をechoすることもできます。実際、どんなPHPコードもBladeのecho文の中に書けます。


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


