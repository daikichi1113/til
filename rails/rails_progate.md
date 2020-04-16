#progateでrailsの復習

2020.4.16<br>
・before_actionを用いてのアクセス制限

2020.4.15<br>
・imegeuploderを使わない画像のDB保存<br>
1)画像の送信】※view<br>
form_tagメソッド<br>
<%= form_tag("送信先のURL", {multipart: true}) %>
inputタグ<br>
<input name="image" type="file"><br>
2)画像の保存】※controller<br>
Ⅰ．ファイル名の保存：@user.image_name = "#{@user.id}.jpg"<br>
Ⅱ．画像の保存：image = params[:image]<br>
Ⅲ．ファイルの保存：Fileクラスのbinwriteメソッド ▶︎ File.binwrite("public/user_images/#{@user.image_name}", image.read)<br>
 

2020.4.14<br>
・フォームの送信先のURLを設定するには、form_tagを利用。<br>
 <%= form_tag("送信先URL") do %><br>
  フォームの中身<br>
 <% end %><br>
・deviseを使わないログイン<br>
・変数sesson/sessionに代入された値は、ブラウザに保存される。<br>

2020.4.13<br>
・renderメソッドは引数に呼び出したいビューのフォルダ名とファイル名を指定する。記述はrender("フォルダ名/ファイル名") 。<br>
 ※ファイル名の部分には拡張子（.html.erb）を書かなくてOK。<br>
・エラーメッセージの取得、表示 ▶︎　@post.errors.full_messages
 

2020.4.12<br>
・paramsは以下の2通りの使い方がある。<br>
 1)「:○○」を使ったルーティングのURLから値を取得する<br>
 2)「name="○○"」が付いたフォームの入力内容を受け取る<br>
・orderメソッド　昇順（:asc）と降順（:desc）

2020.4.11<br>
・consoleの基礎の曖昧だった部分が明確になった。<br>
・erb表記<% %><%= %>の再確認