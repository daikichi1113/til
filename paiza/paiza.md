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
nums = gets.split.map(&:to_i)

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