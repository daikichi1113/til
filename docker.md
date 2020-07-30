# dockerとは
コンピュータ上にコンテナと呼ばれる箱を作ってそこにOSや他のソフトを入れてあたかも違うコンピュータのように扱えるもの

１つのコンテナをメンバーで共有することで同じ環境で開発ができる

## 省エネ
一種の仮想化といえる技術。
従来の仮想化技術(サーバ仮想化)に比べDockerの仮想化(コンテナ仮想化)は軽量でプロセッサやメモリの消費が少なくストレージの使用もわずか

サーバ仮想化→それぞれのOSを立ち上げてそれぞれのAppを動かしている
コンテナ仮想化→仮想マシンごとにOSを立ち上げない．

## できること
・アプリ開発環境の構築
・マイクロサービスの実行環境の構築

# Dockerの始め方

## Docker Hubに登録
MacでDockerを使う場合はDocker Desktopというアプリをインストールする。そのためにDocker Hubのアカウントを作成する。

※Docker Hub　Docker HubはDocker imageを管理する場所（githubのようなもの）

## Docker image
Docker HubにはDocker imageが保管されてる

Dockerfile⇨Docker image⇨コンテナの流れで作られる．

# コマンド
docker login : ログイン
docker pull {image} : docker hubからpullする
docker images : image一覧
docker run {image} : imageからコンテナを作る
docker run -it {image} bash : imageからコンテナを作って中にはいる
exit : コンテナから出る
docker ps -a : ホストにあるコンテナ一覧表示
docker images : ホストにあるイメージ一覧表示
docker restart : exited状態のコンテナを再起動(Up状態に)する
docker exec -it {container} bash : Up状態のコンテナに入る
docker commit {container} {image} : コンテナを指定して新しいイメージを作る
docker tag {source} {target} : imageを新しい名前にタグづけする
docker push {image} : docker hubにpushする
imageを削除する：docker rmi イメージ名

## docker pull
docker hubからホスト（ローカル環境）へimageをpullする

## docker images
ホストのimage一覧

REPOSITORY|TAG|IMAGE ID|CREATED|SIZE|
hello-world|latest|bf756fb1ae65|6 months ago|13.3kB

## docker run
pullしたimageからコンテナを作る
ただし、オプションをつけずに実行すると作成したあとのexited（コンテナから出る）。

コンテナの中に入るには、
docker run -it {IMAGE名:TAG名} bash

※コンテナは、「使って消す」という使われ方と「残したまま使う」という使われ方の２種類がある。
※コンテナの中にあるimageを実行できる命令を出せるのがbash

## docker ps
コンテナ一覧。
docker ps：activeのコンテナだけ表示
docker ps -a : all（全ての）コンテナを表示

CONTAINER ID|IMAGE|COMMAND|CREATED|STATUS|PORTS|NAMES|
dd3d542f7b89|hello-world|"/hello"|4 minutes ago|Exited (0) 4 minutes ago|upbeat_diffie|

# 気をつけること
ホストにいるのか、コンテナにいるのか
dockerを起動するとデフォルトでroot権限になる

# docker imageの成り立ち
docker imageはdocker layerが重なってできている。
※複数のコンテナで１つのimageを共有する = 省スペース

# Docker imageをrunしコンテナを作る→コンテナを更新してホストに戻る

## pullしたimage
docker image ----
              | docker layer
              | docker layer
              | docker layer
              --

## pullしたimageからコンテナを作る/コンテナに入って何かを更新する
新たにdocker layerが上乗せされる。

コンテナ -------------------
          docker layer ←コンテナ作成時に新しく追加されたlayer
                         ここに新しい情報を追加していく

          docker layer ←pullしたimageのlayer
          docker layer 
          docker layer
        -------------------

## コンテナから出る
exit : exitコマンド
        コンテナを動かすprocessを切って出る（statusがExitedになる）
detach : ctrl + p + q　注）ショートカット（statusがUpのまま）
        processを残したまま出る
        元のprocessでコンテナに入るには docker attach <コンテナID（CONTAINER ID） または 名前（NAMES）>

# コンテナをrestart（再起動）する
・dockerを再起動する
docker restart <コンテナID（CONTAINER ID） または 名前（NAMES）>
・再起動したコンテナの中に入る
docker exec -it <コンテナID（CONTAINER ID） または 名前（NAMES > bash 

※Dockerは特に指定がなければ勝手にコンテナに名前をつける

# コンテナをcommitしてレジストリにアップロードする
docker commit {コンテナ名またはID} {新しいDocker image名}
※コンテナ外で実行する

# docker hubにdocker imageをpushする
## docker hubにリポジトリを作る
自分用の亜tららしいリポジトリを作る（他人が作成したリポジトリは、許可がない限りpullしたリポジトリにアップはしないこと）
１つのimageに対して１つのリポジトリが割り当てられる

・docker hubのwebページで作る
create リポジトリ

### IMAGE名
IMAGE名　＝　REPOSITORY名 または REPOSITORY名:TAG名　※TAGがない場合はlatest

イメージの名前とリポジトリの名前は一致していないといけない

## docker imageを別名で保存する
why?
・１つのimageに１つのリポジトリ
・dockerはイメージの名前でpush先を探す
　→そのため、イメージの名前とリポジトリの名前は一致していないといけない

docker tag {sourse(現在のIMAGE名）} {target(<username>/IMAGE名}
※同じimageに対して別の名前（tag)をつける

## リポジトリにpushする
docker push イメージ名(リポジトリ名)

pullしてきたlayerはリポジトリにpushされない
　why? 元々のリポジトリと共有しているため。参照し合う。

# docker hubにpushしたimageをpullする
docker pull
※自分のリポジトリのTagsのなかにコマンドがあるのでコピーして使うと間違えない


# コンテナをもっと理解する
