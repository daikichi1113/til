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