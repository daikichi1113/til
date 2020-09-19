# ファイルを選択する
git add ファイル名

# 選択したファイルを記録する
git commit -m "メッセージ"<br>
コミットメッセージは他の人が見たときに、どんな変更を行ったかが分かりやすいように

# リモートの URL を登録する
git remote add リモート名 URL

# リモートにファイルをアップロードする(push)
git push origin master

# リモートのファイルをダウンロードする(pull)
git pull origin master

# 共同開発の流れ
 add ▶︎ commit ▶︎ push ▶︎ pull ▶︎ add ・・・

# 自分が変更したファイルのファイル名を表示する
git status<br>
add されたファイルが緑色、まだ add されていないファイルが赤色で表示される

# 変更内容を把握
git diff

# 自分や他人のコミットを確認する
git log<br>
※変更内容が見たければ、git log -pを使う。<br>
表示内容が多い時は特殊な表示モードになる。上下キーを使うと表示範囲を変えられて、Qキーを押すことで終了できる

