# laravelはcomposerで動く

# プロジェクト作成
composer create-project laravel/laravel プロジェクト名

※WEB環境があるところで実行すること<br>
※インストールが完了するとkeyがコマンドラインに表示されるので、必ずどこかにコピーを取っておくこと。（プロジェクトディレクトリ内のファイルがわかりやすい）

# ローカルでWEBサーバー起動
php artisan serve

# マイグレーション
## マイグレーションファイルの作成
php artisan make:migration テーブル名_table

※場所はdatabaseディレクトリ→migrationsディレクトリの中。標準でユーザーとパスワードのマイグレーションファイルが用意されている。

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

# データベース設定
設定ファイル　config→database.php

１）使用するSQL設定
'default' => env('DB_CONNECTION', 'mysql'),

デフォルトはmySQL。SQLを変更したい場合はmySQLの部分を書き換える。

２）データベースの設定


## 実行
php artisan migrate

マイグレートを実行して、以下のエラー分が出た場合

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