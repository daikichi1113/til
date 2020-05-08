# 複数行データの標準入力の取得
## 標準入力から複数行データを読み込む基本形<br>
count = gets.to_i<br>
puts("データ個数 #{count}")<br>

for i in 1..count<br>
line = gets<br>
puts "hello #{line}"<br>
end<br>

## 1行目に取得対象のデータ数(行数)を表す整数があって、2行目以降に取得対象のデータを変数arrayに配列として取り組む場合
num = gets.to_i
array = []
while s = gets
  array << s.sub(/\R/,"")
end
p array

# N倍の文字列
"文字列" * 数値　で　数値の回数"文字列"が並ぶ<br>
例）"*" * 4 = ****<br>

# 奇数か偶数か
N % 2 == 0<br>
 ture　▶︎　偶数<br>
 false　▶︎　奇数<br>

# nまでの和
s = 0<br>
i = 1<br>

while i <= n do<br>
  s = s + i<br>
  i += 1<br>
end

# N回ゲーム
while i <= N do<br>
  sum = i<br>
  i += 1<br>
end<br>

# N文字目まで出力
S.slice(n-1)<br>

# サイコロの裏面
7-n<br>

# 運賃の計算
100 + (N * 10)<br>

# 割った余り
N % M<br>

# leet変換
s.gsub!(/A/,'4')<br>

【文字の置き換え】<br>
gsubは正規表現にマッチした部分をすべて変換するメソッド<br>
string = "ruby ruby ruby"<br>
puts string.gsub(/ruby/, 'python')<br>

gsubの破壊的メソッドがgsub!<br>
string = "ruby ruby ruby"<br>
string.gsub!(/ruby/, 'python')<br>
puts string<br>

# 点数の計算
input.split(" ")<br>
score[0].to_i + score[1].to_i + score[2].to_i<br>

# イニシャル
name.split.map{|s| s[0]}.join('.').upcase

splitメソッドは、文字列を分割し、配列にする。<br>
mapメソッドは配列に対して、同じ処理を繰り返し行う。<br>
joinメソッドは、配列の要素を文字列に変換し、引数を区切り文字として、結合した文字列を返す。<br>
upcaseメソッドは、小文字を大文字に変更する。<br>

# ポイント払い
for i in 1..M do

# 小文字を大文字に
文字列.upcase!<br>

大文字を小文字に<br>
文字列.dawncase!

# 文字を切り詰める
sliceメソッドは、文字列・配列の中から任意の範囲を抽出する

# 文字列の一致
==<br>
!=

# 逆さ読み
.reverseメソッドは文字列を文字単位で左右逆転した文字列を返す

# 長さの一致
.lengthメソッドは文字列の長さを数値で返す

# アットマーク
文字列の置換<br>
 sub/sub! 最初にマッチした最初の一箇所を置換<br>
 S.sub(/at/, '@')<br>

 gsub/gsub! 正規表現にマッチした部分をすべて変換する<br>
 S.gsub(/at/, '@')

# 文字の反転
.reverse

# 単語の省略
delete メソッドを使うことで、指定した文字を文字列から削除できる<br>
文字列.delete("削除したい文字")

# N番目の単語
一行で複数の値入力のケースについて<br>
num = gets.split.map(&:to_i)

１．getsメソッドで値入力を受け取り<br>
２．splitメソッドで文字列として配列に格納<br>
(３．mapメソッドを用いて各要素を整数型に変換)<br>

# ゲームのスタミナ
一行入力の値を配列で取得→ N = 配列[0],M = 配列[1]

# プレゼント選び

# 税率の変更
.to_i 整数を返す<br>
.to_f 少数を返す<br>

少数の計算の答えを整数で返す場合、式にto_iメソッドをつける<br>
puts (p + (p * y)).to_i - (p + (p * x)).to_i

# 区切り文字の統一

文字列（二文字以上）の出現回数を数える<br>
.count
.scan 一致する文字列を抽出して配列にする<br>
 →s.scan('ruby').length　※lengthメソッドで配列の中身を数える

# 自動でチャージ
単純なif文

# ボーナスの計算
一行で複数の値入力のケースについて<br>
num = gets.split.map(&:to_i)

# おかしの二等分
演算子<br>
%は割った余り、/は割った答え<br>
N ％ 2 == 0 は２で割り切れる

# かまくらづくり
3乗　r1 = num[0]*num[0]*num[0]

# 数字の桁数
lengthメソッド　文字数を数えてその値を返す

# ピラミッドの作り方
1からnまでの数字を足す<br>
n = gets.to_i<br>
num = 0<br>
for i in 1..n do<br>
  num += i<br>
end<br>
puts num<br>

# 鉛筆の数

# 試合の回数

# 絶対値を求めよ
.absメソッド

# 温度差の計算

# Eメールアドレス

# 家族で分ける
num = gets.split.map(&:to_i)

# 分から秒へ
num = gets.split.map(&:to_i)

# 忘年会の予算
num = gets.split.map(&:to_i)

# 計算機の表示

# ログのフィルター
文字列の中に、指定した複数の文字列が含まれるか確かめる方法<br>
include?メソッド

# AボタンとBボタン

# 日付のデータ

# 西暦の計算

# 契約の交渉
.scanメソッドと.lengthメソッドの併用<br>
scan 一致する文字列を抽出して配列にする<br>
length 文字数を数えてその値を返す<br>
s.scan('y').length

# 文字列を囲う
"#{変数}"

# スイッチのオンオフ
奇数か偶数か　N % 2 == 0　※２で割り切れるかどうか

# 短冊づくり
.char 文字列に対してcharsメソッドを使用すると1文字ずつ分割<br>
※文字列が数字だと、他のメソッドと組み合わせることで「各位を足しあわせた合計値」なんて操作もできるようになる<br>
list = "12345".chars.map(&:to_i)<br>
p list.sum

# AからRへ
指定した文字列を数える　.count/.scan<br>
文字列の置換　.subメソッド<br>
if X.count('A') == 0<br>
    puts X<br>
else<br>
    puts X.sub(/A/, 'R')<br>
end<br>

# こよみの変換

# 本棚選び

# ジュースの分配

# 残りのページ

# 空港の呼称
.slice(0..2)

# 花粉の予報
gets.chomp
.count("12")

# 充電時間

# 表面積の計算

# 天気の表示

# 送料の計算

# カウントダウン
繰り返し文と演算子で１ずつ引く<br>
while N > 0 do<br>
    puts N<br>
    N = N - 1<br>
end

# 正三角形かどうか
かつ　a == b && a == c

# 梅雨入りの予想
文字列から１を抜き出して数える　※文字列なのでgets.chomp
num.scan('1').length

# お月見団子
配列[0]と配列[1]でそれぞれif文

# アルファベットで何番目
indexメソッド<br>
レシーバであるオブジェクトが、<br>
文字列の場合は引数である部分文字列が最初から何番目にあるかを整数で返す。<br>
オブジェクト.index(“検索したい部分文字列”)<br>
配列の場合はその要素が最初の要素から何番目にあるのかを整数で返す。<br>
配列.index(“検索したい配列の要素”) <br>
注意:最初は０番目から数える。

# 最大と最小
配列.max<br>
配列.min<br>
入力された値を配列に。array = [n_1, n_2, n_3, n_4, n_5]

# 一週間の予定
入力された値を配列に。その後、countメソッド。<br>
array = [d_1, d_2, d_3, d_4, d_5, d_6, d_7]<br>
puts array.count('no')

 # 雨と晴れの記録

 # 画面の残り

 # Aの個数
.count('A')

# 初詣で
L = 'A'*i[0]
M = 'B'*i[1]
N = 'A'*i[2]
puts L+M+N

# お菓子のプレゼント

# 足りないカード
.include?
