# linux
Unixから派生したOS
※macはUnixベースのOS
→ macでLinuxコマンドを学習する

## シェル（shell）
ユーザーの命令はkernel（核）ではなく、shell（殻）に出す
<流れ>ターミナル→shell→kernel

ターミナル：shellを動かすためのアプリ
shell：kernelに接続するためのツール

## shellの種類
bash,zsh,sh ...

## 環境変数
OSで動くプロセスが情報を共有するために使う
＄文字列で表示

## shellの環境変数
echo $SHELL　※shellの種類がわかる

## linux基礎コマンド
cd :ディレクトリを移動する
pwd : 今いるディレクトリを表示
mkdr : 新しいディレクトリ（ファイル）を作成
touch : 新しいファイルを作成
ls : カレントディレクトリのファイル、フォルダを一覧表示
rm ファイル名 : ファイルを削除
rm -r フォルダー名 : フォルダーを削除
reset : ターミナルの表示をリセットする

## Linux catコマンド
cat {file名} : ファイルの閲覧
cat {fileA} > {fileB} : fileAの情報をfileBに上書き保存
cat {fileA} >> {fileB} : fileAの情報をfileBに追加保存
cat {fileA} {fileB} : fileAとfileBを連結（保存はしない）

【catコマンドのオプション】
-n（--number）
　cat -n fileB：行番号をつけて出力
-b（--number-nonblank）
　cat -b fileB：blankなし（空白行を入れずに）番号をつけて表示する
-s（--squeeze-blank）
　cat -s fileB：連続した空白行を１行の空白行にまとめる
-E（--show-ends）
　cat -E fileB：各行の最後に"$"を表示する
-T （--show-tabs）
　cat -T fileB：タブを"^I"に置き換えて表示する

【catに類似したLinuxコマンド】
・tacコマンド：catの逆順で表示
　tac {file名}

・lessコマンド：ファイルの閲覧

## 「less」と「tail」「cat」の使い分け
ファイル閲覧をする場合:less
スクリプトや設定ファイルなどを閲覧のみしたい場合は、誤って上書きするリスクがない「less」コマンドがおすすめです。

ログの監視の場合:tail
ログファイルは通常行数が多いので、ファイル末尾だけを表示してくれる「tail」コマンドに「-f」オプションをつけるのがおすすめです。

文字列を検索・ファイルを表示する場合:cat
文字列を検索する場合は、「cat」コマンドにパイプで「grep」コマンドを使うのがおすすめです。また、ファイル全体を表示するのにも「cat」コマンドが使えます。