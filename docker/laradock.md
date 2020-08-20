# Laradockとは
Laravel(PHP)のプロジェクトをDocker上で動作させるための開発環境

仮装の開発環境内ではphpコマンド、laravelコマンドが使える。

## なぜ仮想環境が必要なのか
Laravelの実行にはいくつものプログラムやライブラリが必要になる（例えばPHP, nginx, MySQLやミドルウェアなど）。そのため仮想のOS環境を用意する必要がある。

Dockerはコンテナ型と呼ばれる仮想環境。

# Laradockの初期環境設定方法
https://qiita.com/don-bu-rakko/items/0297280553e99aa6d7b8

## laradockをcloneする
git clone https://github.com/LaraDock/laradock.git
  //githubからlaradockをgit cloneする。

laradockディレクトリが作成されるので移動

## .envファイルの作成
cp env-example .env
  //cpコマンドを用いて、.envファイルを作成

## .envファイルの編集
MySQL（DB）のバージョン指定。

もし、プロジェクト毎に新しいlaradock環境を作りたい場合は、下記の変数をユニークなものに変更。
# Define the prefix of container names. This is useful if you have multiple projects that use laradock to have seperate containers per project.
COMPOSE_PROJECT_NAME=laradock

データの保存先をlaradock毎に分離したい場合は DATA_PATH_HOST を書き換え
# DATA_PATH_HOST=~/.laradock/data
DATA_PATH_HOST=.laradock/data

## コンテナを作成する
docker-compose up -d nginx mysql
  //-dオプションはdetatchedの略で、バックグラウンドでコンテナを実行する
  //使うコンテナだけを指定しないと時間がかなりかかる

コンテナが立ち上がったらdocker psコマンドで起動しているか確認

## Workspace上にLaravelを立ち上げる
・workspaceに入る（laradockユーザーでログイン）
docker-compose exec --user=laradock workspace bash
// ログイン後のユーザー名がlaradock@...となっていればOK

・ログイン状態でcomposerコマンドを用いてLaravelをインストール
composer create-project laravel/laravel {アプリ名}

・ログイン状態でlsコマンド実行。ディレクトリが作成されているか確認
　exitコマンドを叩いて、仮想環境から抜け出す

## 作成したアプリ名ディレクトリの.envファイルを編集
DB_HOST=mysql # 127.0.0.1 から変更
DB_DATABASE=default # laravel から変更
DB_USERNAME=default # root から変更
DB_PASSWORD=secret

## laradockディレクトリの.envを編集
APP_CODE_PATH_HOST=../　をアプリ名のディレクトリ名に

## dockerを再起動
docker-compose stop
docker-compose up -d nginx mysql

http://localhost/ にアクセスしてLaravelのTop画面が出てきたら成功

## 再度仮想空間に入る（rootで）
docker-compose exec workspace /bin/bash

