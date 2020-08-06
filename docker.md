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
自分用のあたらしいリポジトリを作る（他人が作成したリポジトリは、許可がない限りpullしたリポジトリにアップはしないこと）
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

## docker run を詳しく解説
docker run {image}
 = docker create（コンテナを作る） + docker start（コンテナのデフォルトコマンドを実行）

## コマンドの上書き
docker run {image} {command}
{command}を変えて実行することで、上書きができる

## -it
docker run -it ubuntu bash

-it
※２つのコマンドオプションをくっつけている
 -i:インプット可能
 -t:表示が綺麗になる

bash を使うために必要なコマンドオプション、という認識で良い

## コンテナの削除
１）コンテナを止める
docker stop {container}
※{container}をスペースで区切流ことで、複数同時に止めることができる.rmも

２）コンテナを削除する
docker rm {container} : 削除
docker system prune : 止まっているコンテナを全削除

dockerを使っているとコンテナが溜まりやすいので、定期的に削除しておくと良い

## コンテナのファイルシステムの独立性
同じimageから複数のコンテナを作成しても、それぞれのコンテナは独立している

## コンテナ名を指定してrunする
docker run --name {name} {image}

どんな時に使うとよい？
・起動させ続けるコンテナを立てる時
・共有サーバを使うとき
・他のプログラムで使用するとき

※同じ名前のコンテナは作成できない（エラーになる）

## detachedモードとforegroundモード
detached mode：コンテナ起動後にdetachする（バックグラウンドで動かす）
[コマンド]docker run -d {image}

foreground mode：コンテナをExit後に削除する（一回きりのコンテナ）
　　　　　　　　　　※不要なコンテナがたまらないようにできる
[コマンド]docker run --rm {image}

注）複数のオプションをつけるとき
docker run -it -d ubuntu bash

# Dockerfile
## Dockerfileとは
Docker imageの設計書で，DockerfileをビルドすることでDocker imageを作成できる。

Dockerfileというtextファイル。"INSTRUCTION arguments"の形で記載する。

※docker hubからDocker imageをpullした場合は既に作ってある。（docker hubで見ることができる）

実業務ではこのDockerfileを使ってDocker imageやコンテナを作ることが多く，DockerfileをメンテすることがDockerを使いこなすことに繋がる

## Dockerfileを作る
ターミナルで作る
・mkdir {dockerfileを作るディレクトリ}
・cd {dockerfileを作るディレクトリ}
・touch Dockerfile

または

vscodeで作る
・vscodeでdockerfileを作るディレクトリを開く
・vscode内でDockerfileを作る

Docker for Visual Studio Code
https://qiita.com/trakkyo/items/c0bde6d5bd12c3f69e51


Dockerfileの中身を記述する
例）
FROM ubuntu:latest
  ///ベースになるDocker image
RUN touch test
  ///ubuntu:latest の上に $ touch test を実行したimage layerを作成

#マークでコメントを書くことができる

### Dockerfileは最後の行に付け加えて更新していく
Dockerfileに記述された各行は各image layerに値するため，基本はDockerfileを更新する際には最後の行に新しい命令文を追加していく．

WHY?
途中の行を変えると，そのあとの行のlayerは全て新しいものとみなされ再度layerが作成さるため．
↓
Dockerfileが大きくなる。
↓
実行するのに時間がかかる。
↓
コンテナを更新するたびにrunするので毎回時間がかかってしまう

そのため，基本は最後の行に付け足していって，時間があるときに綺麗にするように心がける

## build（Dockerfileからdocker imageを作る）
docker build {ディレクトリ名}　：　ディレクトリ内のDockerfileというファイルを探してビルドする
※カレントディレクトリの場合は docker build . 
　　　　　　　　　　　　　　　　　↑の形でbiludするのが一般的。

ターミナルの最後に表示されている文字列がimageのIDとなる
例）Successfully built 868fd2d6c226
　　　　　　　　　　　　　　↑ココ

※docker buildでビルドされたimageはimage名（リポジトリ名：タグ名）がnoneになっているため、dangling imageと呼ばれる

### オプションで名前をつけてビルドする
dangling imageを避けるには、オプションで名前をつけてbiludする

docker build -t {IMAGE名} {ディレクトリ名}

例）docker build -t new-ubuntu:latest .
　　　　　　　　　　　　↑image名 = リポジトリ名：タグ名
　　　　　　　　　　　　　　　　　　　　　　↑.でカレントディレクトリを指定

ターミナルの最後にIDとイメージ名が表示される
例）
Successfully built 868fd2d6c226
Successfully tagged new-ubuntu:latest

## ビルドしたDocker imageをrunしてコンテナに入る
docker run -it image名 bash
 
## Dockerfileからimageを作る利点
・Dockerfileからimageをbuildする
　▶︎　Docker fileが存在する = チーム内で設計書を共有できる

・コンテナを直接変更してimageにcommitする
　▶︎　Docker fileが存在しない = チーム内で設計書を共有できない

簡易図解：

Dockerfile　：　textファイル。Docker imageを作る設計図 

   ↓ build

Docker image　：　コンテナを作るためのもの。携帯して配布できる
 ↓      ↑
 ↓ run  ↑
 ↓      ↑ commit　：　コンテナを更新してDocker imageにすることも可能
 ↓      ↑
コンテナ　：　実際に開発したりアプリを実行する場所。
　　　　　　　docker imageから簡単に作ったり消したりできる

## Dockerのもっとも重要なスキル
Dockerfileをメンテすること
※コンテナを更新するときはなるべくDockerfileをメンテする

# Dockerfileの書き方
Dockerfileの基本的なinstruction（命令）

・FROM
・RUN
・CMD

## FROM
・ベースとなるimageを決定。このimageの上にレイヤーが重なっていく。
※DockerfileはFROMから書き始める

※必要最低限のDocker imageを入れるようにする

参考：build実行後のターミナル表示
Sending build context to Docker daemon  2.048kB
Step 1/2 : FROM image
 ---> 1e4467b07108             /// imageのID
Step 2/2 : RUN touch test
 ---> Using cache
 ---> 868fd2d6c226             /// layerのID（imageの上に重なる）
Successfully built 868fd2d6c226
Successfully tagged new-ubuntu:latest

## RUN
・RUNに続くLunuxコマンドを実行
※RUNを使うことで好きなようにカスタマイズできる
※RUN毎にlayerが作られる

参考：
FROM ubuntu:latest
RUN touch test
RUN echo 'hello world' > test

--
layer / echo 'hello world' > test 
--
layer / touch test
--
layer /  ベースのimage（ubuntu:latest）

### layer数を最小限にするために
RUN,COPY,ADDのインストラクション（命令）はlayerを作る。
特にRUNが多くなる。
→インストラクションを増やせば増やすほどlayerが増える
→コンテナが重くなる

だから

Docker imageのlayer数は最小限にする！

方法：コマンドを&&でつなげる
     バックスラッシュで改行する(複数インストールしたパッケージをみやすく)
     　※アルファベット順に並べるとみやすくなる

例）
FROM ubuntu:latest
RUN touch test
RUN echo 'hello world' > test
↓
FROM ubuntu:latest
RUN touch test && echo 'hello world' > test

## Ubuntuでパッケージ管理する
１）apt-get update:新しいパッケージリストを取得
２）apt-get install {package}:packageをインストール

例:layerを最小限にする）
FROM ubuntu:latest
RUN apt-get update
RUN apt-get install xxx
RUN apt-get install yyy
RUN apt-get install zzz
↓
FROM ubuntu:latest
RUN apt-get update && apt-get install -y \
xxx \
yyy \
zzz

※-y インタラクティブな質問に全てyesで答えるオプション。dockerでinstallする場合は選択肢を選べないのでオプションをつける

## キャッシュ（cache）
Dockerfileを作る・メンテナンスするときはキャッシュをうまく利用する

【例】
・１回目のbuild時のDockerfile
--
FROM ubuntu:latest
RUN apt-get update
RUN apt-get install -y \
    curl \
    nginx
--
buildすると、上記の２つのRUNがキャッシュに残る

・Dockerfileにパッケージを追加インストール追記
--
FROM ubuntu:latest
RUN apt-get update
RUN apt-get install -y \
    curl \
    nginx
RUN apt-get install -y \
    cvs
--
buildすると上２つのRUNはキャッシュを参照するため実行されない
追記したRUNだけ実行され、パッケージがインストールされる

・キャッシュが通ることが確認できたので、DockerfileのRUNをまとめてlayerを１つにする
--
FROM ubuntu:latest
RUN apt-get update && apt-get install -y \
    curl \
    cvs \    ///パッケージはアルファベット順に並べる
    nginx
--

## CMD
CMD:コンテナのデフォルトのコマンドを指定

構文
CMD["executable(コマンド)","param1(引数2)","param2(引数2)"・・・]
※引数が必要なときは上記のように記述する
※Dockerfileの最後に記述する（原則）

例）
FROM ubuntu:latest
RUN apt-get update && apt-get install -y \
    curl \
    cvs \
    nginx
CMD ["ls"]

## RUNとCMDの違い
RUNはlayerを作る
CMDはlayerを作らない

# docker buildの詳細
## docker buildは何をしているのか
docker build .　コマンドでなぜディレクトリを指定しているのか？

docker buildコマンドで行っていること
・dockerfileのあるディレクトリをコピー
・コピーしたディレクトリをbuild contextとしてdocker daemonに渡す
・docker daemonがbuild context（ディレクトリ）を元にimageを作る

build contextの中にあるファイルはbuild時に使うことができるため、ディレクトリを指定する。

## docker daemonとは
dockerのアーキテクチャ（構造）はclient-server アーキテクチャ。

client(コマンドで操作する場所)
 docker build
 docker pull
 docker run

Docker HOST（サーバー側。実際に実行している場所）
 ・docker daemonがある。clientからの命令を実行する。
 ・imageを作る、コンテナを作る

## build contextとは
build context = build時のディレクトリの状態

※buildに関係のないフォルダやファイルは置かない。
※build contextの中にあるファイルやフォルダはdocker deamomに渡すことができるが、docker imageには反映されない。
反映させるためにはdockerfileにADDやCOPYのインストラクションを記述する必要がある。

## COPY
docker instructionの１つ。layerを作る。
build contextにあるファイルをdocker imageに反映させる。

dockerfileへの記述
COPY {sorce(ファイル名)} /{反映させる先（ディレクトリ名）}

例）
// dockerfile
FROM ubuntu:latest
RUN mkdir /new_dir
COPY something /new_dir/

## ADD
dockerfileへの記述
ADD {sorce(ファイル名)} /{反映させる先（ディレクトリ名）}

## COPY と ADD
・COPY／単純にファイルやフォルダをコピーする場合
・ADD／tarの圧縮ファイルを解凍したいとき

### 知っておくと便利なコマンド
echoコマンド：ファイルに文字列を入れる
　echo '文字列' > ファイル名

tarコマンド：tarファイル（圧縮ファイルを作る）
　tar -cvf 圧縮ファイル名 圧縮するファイル

mvコマンド：ファイルを移動する
　mv 移動元のディレクトリ／ファイル名 移動先のディレクトリ／ファイル名

　※mvコマンドを活用してファイル名の変更も可能
　mv ディレクトリ／現在のファイル名 ディレクトリ／新しいファイル名

## Dockerfileがbuild contextにない場合
docker build -f {dockerfilename} {buildcontext} ディレクトリ名

例えば...同じbuild contextを使ってbuildするDockerfileが複数ある場合などに使う。

docker dir-|-Dockerfile.div
           |-Dockerfile.test
           |-sample dir *dockerfileのないbuild context      

// sampleディレクトリ
docker build -f ../Dockerfile.div sample dir

*.はカレントディレクトリ、..は１つ上のディレクトリ 

## CMD と ENTRYPOINT
どちらもデフォルトコマンドを指定することができる。

●何が違うのか
・run時のコマンドの上書き
 CMD:できる  docker run image名 上書きするコマンド 
 ENTRYPOINT:できない。ただし、オプション部分は可能
   docker run image名 上書きするオプション
   → 上書きして欲しくないコマンドに使うと良い。

●ENTRYPOINTがある場合
 CMDはENTRYPOINTで指定したコマンドの引数をとる
 つまり、ENTRYPOINTがある場合のCMD少し役割が変わり、ENTRYPOINTで指定した
コマンドの引数だけを書くことになる。

例）
// Dockerfile(CMDのみ)
FROM ubuntu:latest
RUN touch test
CMD ["ls", "--help"] //コマンドとその引数

// Dockerfile(ENTRYPOINT有り)
FROM ubuntu:latest
RUN touch test
ENTRYPOINT ["ls"] // コマンド
CMD ["--help"] //ENTRYPOINTのコマンドの引数

ENTRYPOINTはコンテナをコマンドのように使いたいときに使う。

## ENV
ENV:環境変数を設定するインストラクション

＜書き方＞
ENV {key} {value}...
または
ENV {key}={value}...

コンテナの中で環境変数を確認するコマンド env

## WORKDIR
WORKDIR:Docker instruction（命令）の実行ディレクトリを変更する

Docker instructionは基本的にルート直下で実行される。
cdコマンドでディレクトリを移動したとしてもルートで実行される。
そのため、WORKDIRが必要になる。

※ただし、&&でcdコマンドを記述した場合は、そのディレクトリで実行してくれる

書き方
WORKDIR /作業するディレクトリ名

cdを安易に使うとバグの元になるので注意。


# ホストとコンテナの関係性

host ←-------→ container
         |
         |
▶︎ファイルシルテムの共有
▶︎ファイルのアクセス権限
▶︎ポートをつなげる
▶︎コンピュータリソースの上限

※全てdocker run コマンド時にオプションで設定

## -vオプション（ファイルシステムの共有）
-v {hostのマウント元のパス}:{container}
 ホストのファイルシステムをコンテナにマウントする。
 ※{container}はなくても作ってくれる。

[重要]
ホストのファイルシステムをコンテナの中にあるように見せる。
※あくまでもホストにある。
実際にはコンテナの中にはないため、コンテナの容量が軽くなる。

例）
docker run -it -v ~/projects/docker_stady/mounted:/new_dir dcdfb6b53f9a bash

## -uオプション
ユーザーIDとグループIDを指定してコンテナをrunする。

ホストのユーザーIDとグループIDを確認する
id -u　ユーザIDの確認
id -g　グループIDの確認

docker run -it -u $(id -u):$(id -g) イメージ名 bash

[重要]
ホストのユーザーIDを指定して実行しているため、ホストのユーザーID情報を共有している状態。ホストのユーザーIDがコンテナのユーザーIDとなっているわけではない。

### パーミッション（アクセス権限）の見方
ls -la: リストの全ファイルの詳細を見ることができる

パーミッション   所有者 所有グループ                ファイル
drwxr-xr-x   5  501 dialout  160 Aug  5 06:01 created_in_Dockerfile
drwxr-xr-x   5 root root     360 Aug  5 07:00 dev

d rwx r-x r-x    /// "r":読取り可 "w":書込み可 "x":実行可 "-"：権限なし
|  |   |   |
|  |   |   その他のアクセス権限 ※読取りと実行はできるが書き込みはできない
|  |   所有グループのアクセス権限
|  所有者のアクセス権限
|
"-":ファイル
"d":ディレクトリ
"l":シムリンク

## -p（publish）オプション
ホストのポートをコンテナのポートにつなげる(publishする)。

ポート：プロセスがデータ通信をするために使うもの。
       建物に例えると、IPアドレスが住所、ポートが部屋番号。

docker run -it -p hostのport番号:containerのport番号 image名 bash

ブラウザでもlocalhost:ホストのポート番号でコンテナを表示させることができる。

## コンテナがアクセスできる上限の設定
--cpus {# ob CPUs} : コンテナがアクセスできる上限のCPUを設定
--memory {byte} : コンテナがアクセスできる上限のメモリを設定

docker run -it --cpus 上限のcpu数 --memory 上限のbyte数 image名 bash

※コンテナのあらゆる情報を表示するコマンド
docker inspect {container}
↓
その中で特定の事項を表示させるにはgrepを使う
docker inspect {container} | grep -i 文字列(cpuなど) |
                                      ↑この文字列を含む情報を抽出する

### MacでCPU・メモリの確認コマンド
物理コア数： sysctl -n hw.physicalcpu_max
論理コア数： sysctl -n hw.logicalcpu_max
メモリ： sysctl -n hw.memsize

※バイト数
1K byte = 1024(2^10) byte
1M byte = 1024 * 1024 byte
1G byte = 1024 * 1024 * 1024 byte 


# docker compose
docker comporse --version

## development
鉄則：１つのコンテナには１つのアプリケーション

## CICD(Test and Deploy)