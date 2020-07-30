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

