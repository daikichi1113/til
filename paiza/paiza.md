# N倍の文字列
"文字列" * 数値　で　数値の回数"文字列"が並ぶ
例）"*" * 4 = ****

# 奇数か偶数か
N % 2 == 0
 ture　▶︎　偶数
 false　▶︎　奇数

# nまでの和
s = 0
i = 1

while i <= n do
  s = s + i
  i += 1
end

# N回ゲーム
while i <= N do
  sum = i
  i += 1
end

# N文字目まで出力
S.slice(n-1)

# サイコロの裏面
7-n

# 運賃の計算
100 + (N * 10)

# 割った余り
N % M

# leet変換
s.gsub!(/A/,'4')

【文字の置き換え】
gsubは正規表現にマッチした部分をすべて変換するメソッド
string = "ruby ruby ruby"
puts string.gsub(/ruby/, 'python')

gsubの破壊的メソッドがgsub!
string = "ruby ruby ruby"
string.gsub!(/ruby/, 'python')
puts string

# 点数の計算
input.split(" ")
score[0].to_i + score[1].to_i + score[2].to_i