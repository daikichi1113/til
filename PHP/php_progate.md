# PHPの書き方
PHPはHTMLに埋め込んで使う。<br>
<?php 〜 ?>の中にPHPの命令を書く。<br>
<?php 〜 ?>の部分がHTMLに変換された上で表示される。

# PHPの文法
文末にセミコロン「;」<br>

# 出力
echo<br>
文字列を出力する場合はシングルクォーテーション「'」かダブルクォーテーション「"」で囲む

# 計算
rubyと同じ

# 変数
頭に「$」記号をつけることによって変数を定義<br>
「$変数名 = 値;」

# 変数名の付け方
英単語、２語以上の場合は大文字で区切る

# 変数に数字を足す
演算子はrubyと同じ<br>
値が１の時だけ、$sum++,＄sum--のようにさらに省略した書き方が可能<br>
変数の前に書く($++sum)とその行の命令が実行される前に足されるのに対し、変数の後に書く($sum++)とその行の命令が実行された後に足される

# 文字列の連結
ドット「.」記号を用いる<br>
「.=」を用いると変数と文字列の連結を省略して書ける<br>
## 変数展開
ダブルクォーテーションで文字列を囲んだ場合、中の変数を{}で囲むとその部分が変数に入っている値で置き換えられます(変数展開)。シングルクォーテーションで文字列を囲んだ場合は変数展開されず、変数が{}で囲まれていてもそのまま文字列としてみなされます。

# if-elseif-else文
if (条件式){<br>
  処理<br>
} elseif (条件式) {<br>
  処理<br>
} else {<br>
  処理<br>
}

# 比較演算子
## 大小
<,<=,>=,>
## 等しいか
==,!=

## 論理演算子
&&（かつ）<br>
||（または）<br>
! 条件の否定 ex) if (!($x == 0))

# switch文
if, elseifによる分岐が多く複雑な場合、switch文で書き換えるとシンプルで読みやすいコードにできる<br>
条件式の値がcaseの後にくる

switch(変数){<br>
 case 0:<br>
  処理；<br>
  break;<br>
 case 1:<br>
  処理；<br>
  break;<br>
 default:<br>
  処理；<br>
  break;<br>
}

# 配列
配列の基本構文「$配列名 = array(値１, 値2, ・・・);<br>
配列のデータを取り出す $配列名[インデックス番号]<br>
値の追加、上書き $配列名[] = 値;

# 連想配列
配列と同じく複数のデータをまとめて管理するのに用いられる。<br>
配列との違いは、個々の要素を管理するのにインデックス番号ではなく、「キー」と呼ばれる文字列などの値を指定することができる点。<br>
$配列名 = array('キー名' => '値１', ・・・);<br>
配列の値を呼び出すときは $配列名['キー名']

# 繰り返し処理
## for文
for (①初期値; ②ループ条件; ④変数の更新) {<br>
  ③繰り返す処理;br>
}

ex)<br>
for ($i = 1; $i <= 100; $i++) {<br>
  echo ＄i<br>
}

※処理を改行して出力する場合は、.'＜br＞'

## while文
①初期化;
while (②ループ条件) {<br>
  ③繰り返す処理;<br>
  ④変数の更新;<br>
}

$i = 1;
while ($i <= 100) {<br>
  $i++;<br>
  echo i;<br>
}

## break文
現在のループを強制的に中断する命令 if文などの条件文と組み合わせて利用する<br>
ex)<br>
for ($i = 1; $i <= 100; $i++) {<br>
  if ($i > 10) {<br>
    break;<br>
  }<br>
  echo ＄i<br>
}

## continue文
現在の周だけをスキップし、ループそのものは継続して実行. 
for ($i = 1; $i <= 100; $i++) {<br>
  if ($i % 3 == 0) {<br>
    continue;<br>
  }<br>
  echo ＄i<br>
}

## foreach文
配列または連想配列に対して、先頭のデータから順に繰り返し処理を行うための命令<br>

foreach (配列 as 値変数) {<br>
  繰り返したい処理;<br>
}

foreach (配列 as キー変数 => 値変数) {<br>
  繰り返したい処理;<br>
}

# 関数
## 組み込み関数
strlen(引数)　文字列の文字数を返す<br>
count(引数)　配列の要素の数を返す<br>
rand(数値,数値)　１つ目の引数と、２つ目の引数の間のランダムな整数を返す

## 関数を自作する
function 関数名(仮引数){ 処理 }<br>
※呼び出しは関数名(引数)

## 戻り値
関数は値を「返す」ことができて、この値のことを戻り値と呼ぶ。関数を実行した結果、その関数実行部分が戻り値に置き換わるというイメージ。<br>
戻り値は「return」で指定

# formタグ
<form action="url" method="get/post"><br>
  フォームの内容<br>
</form><br>

## 1行のテキストボックス
<input type="text" name="データベース用の名前"><br>
<input>タグは閉じタグが必要ない

## 改行含むテキストボックス
<textarea name="データベース用の名前"></textarea>

## 送信ボタン
<input type="submit" value="ボタンに表示される値">

## フォームのデータを受け取る
$_POST<br>
「$_POST」は連想配列。<input>と<textarea>のname属性に指定した値を入れることで、それぞれの送信した値を受け取ることができる

## セレクトボックス
セレクトボックスをつくるには<select>タグの中に<option>タグを並る。
すると<option>タグの中身が選択肢として表示される。

セレクトボックスの値の渡し方<br>
<select>タグに「$_POST」で値を受け取るためのname属性を指定。<br>
<option>タグのvalue属性が送信される値。

ex)<br>
<select name="fruit"><br>
  <option value="apple">りんご</option><br>
</select><br>

## 繰り返し処理と変数展開を用いて多数のoptionタグを作る。
<?php <br>
  for ($i = 6; $i <= 100; $i++) {<br>
    echo "<option value='{$i}'>{$i}</option>";<br>
  }<br>
?><br>

変数展開を用いる際はダブルクォーテーションで囲むように。

## foreach文と文字列の連結を用いて、配列$typesのoptionを表示
<select name="category"><br>
  <option value="未選択">選択してください</option><br>
  <?php<br>
    foreach ($types as $type) {<br>
      echo "<option value='{$type}'>{$type}</option>";<br>
    }<br>
  ?><br>
</select>

# クラスとインスタンス
## クラスの定義
「class クラス名」と定義し、「{}」の間に、そのクラスの内容を書く<br>

## インスタンスの生成
new クラス名()<br>
$変数名 = new クラス名()」のようにすることで生成したインスタンスを変数に代入<br>
インスタンスの生成はクラスの外で.

# プロパティとメソッド
## プロパティ
プロパティとはインスタンスが持つデータのこと<br>
定義 public $プロパティ名<br>
プロパティへのアクセス インスタンス->プロパティ名（プロパティ名に$は不要）<br>

例）<br>
$menu = new Menu();<br>
$menu->プロパティ名 = 'value';  *プロパティに値をセット<br>
echo $menu->プロパティ名;  *セットした値にアクセス

## メソッド
メソッドはインスタンスに関連する処理（関数）のこと.それぞれのインスタンス固有<br>
定義　public function メソッド名(){処理}<br>
呼び出し　インスタンス->メソッド名()
　　　　　例）$this->hello();

# $this
メソッド内でインスタンスのプロパティやメソッドにアクセスしたい時には「$this」という特殊な変数を用いる<br>
$thisはクラス内のメソッドの定義の中でのみ使用できる。<br>
$thisはメソッドが呼ばれた時に、そのメソッドを呼び出しているインスタンスに置き換えられる<br>

# コンストラクタ
__construct *アンダーバー２つで始まる<br>
インスタンスの生成時に呼ばれるメソッドのこと<br>
public function __construct() {処理;}

## コンストラクタと引数/コンストラクタとプロパティ
__constructメソッドは引数をとることができる<br>
__constructメソッド内で、$thisを用いてインスタンスのプロパティに値をセットすることができる<br>

例）<br>
<?php<br>
class Menu {<br>
  public $name;<br>

  public function __construct($name) {<br>
    $this->name = $name;<br>
  }<br>
  
  public function hello() {<br>
    echo '私は'.$this->name.'です';<br>
  }
}

$curry = new Menu('CURRY');<br>
$pasta = new Menu('PASTA');<br>

$curry->hello();<br>
echo '<br>';<br>
$pasta->hello();<br>

?><br>

# HTMLとPHP
## HTMLにPHPのコードを埋め込む
PHPのコードを埋め込むことで、HTMLのコードとPHPのコードを切り分けることができ、見やすくなる<br>
<p><?php echo $curry->name ?></p>

## foreach文をHTMLに埋め込む
foreach文の「{」の代わりに「:」、「}」の代わりに「endforeach」と記述し、その間に処理を書く。<br>
この処理部分にはHTMLのタグを書くことができるので便利。<br>

<?php foreach ($menus as $menu): ?>
 <h3><?php echo $menu->name ?></h3>
<?php endforeach ?>

## if文、for文、while文や、witch文をHTMLに埋め込む
それぞれ「endif」、「endfor」、「endwhile」、「endswitch」を使って書く<br>
※elseを用いる場合はif():~else:~endif<br>
注）//elseの後に:が必要

# require_once
「require_once」を用いると別のphpファイルを読み込むことができる<br>
require_onceで読み込んだファイルで定義されているクラスや変数をrequire_onceを記述したファイル内で使うことができる<br>

<?php require_once('data.php') ?>

# 画像表示

imageプロパティの値は<img>タグのsrc属性に指定するため、クォーテーションの中に埋め込む。<br>
また、echoをしないとphpの処理の結果が出力されず、HTMLに反映されないので注意<br>

# floor関数
floor(); *小数点以下を切り捨てた値が得られる<br>
echo floor(1.5);<br>
* 結果=> 1

# カプセル化
オブジェクト指向の重要な機能の１つで、使い手に必要ないものを隠してしまうこと<br>
クラスのプロパティとメソッドへのアクセスを制限することを言い、クラスの外部からアクセスできるようにするには「public」を、アクセスできないようにするには「private」を用いて定義する。<br>
プロパティは基本的にアクセス権をprivateにする
## アクセス権限
public
private

## ゲッター
プロパティの値を返すだけのメソッド<br>
ゲッターは「getプロパティ名」のように命名するのが一般的
  public function getName() {
    return $this->name;
  }

## セッター
プロパティの値を変更するメソッド<br>
「setプロパティ名」のように命名するのが一般的

# プロパティの初期値
プロパティを定義する際には初期値をセットすることができる

# inputタグの初期値
<input>タグにvalue属性を用いると初期値を設定することができる。
初期値に指定した値がテキストボックスに最初から表示される。

# フォームの値を受け取る
<input>タグのname属性はそれぞれのMenuインスタンスのnameプロパティなので、nameプロパティの値を用いて送信された値を受け取る

# クラスプロパティ
クラスがもつデータ。<br>
クラスプロパティは「static」を用いて定義する。<br>
class Menu {<br>
  public static $count = 4;

クラスプロパティにアクセスする場合 「クラス名::$クラスプロパティ名」<br>
<?php echo Menu::$count ?>

インスタンスの数は個々のインスタンスではなくクラス全体で管理する必要があり、「クラスプロパティ」というものを用いると実現できる。

# クラスメソッド
## コンストラクタの活用
$countの初期値を0として、コンストラクタ内でクラスプロパティ$countの値に1を足すことで、生成されたインスタンスの数を数えることができる<br>
Class Menu {
  public static $count = 0;
  public function __construct(...){

  }
}

## クラス内でクラスプロパティにアクセスする(self)
selfはクラスの中で使うとそのクラス自身のことを指し示し、「self::$クラスプロパティ名」のように使う<br>
Class Menu {
  public static $count = 0;
  public function __construct(...){
    self::$count++;
  }
}

## 個々のインスタンスのデータに関係ない処理を行う
クラスメソッドは「static」を用いて定義し、「クラス名::クラスメソッド名」のように呼び出す<br>
Class Menu {
  private static $count = 0;
  public function __construct(...){
    self::$count++;
  }
  public static function getCount {
    return self::count;
  }
}

echo Menu::getCount(); //クラスメソッドの呼び出し

# 継承
すでに定義されているクラスのプロパティやメソッドを別のクラスに引き継ぐこと<br>
元のクラス▶︎「親クラス」<br>
継承してできる新しいクラス▶︎「子クラス」<br>
子クラスは、親クラスのプロパティやメソッドを全て引き継いだ上で、独自の機能を追加することができる

## 継承の書き方
class 子クラス名 extends 親クラス名

# 独自メソッド、プロパティ
## 独自プロパティ
子クラスには独自のプロパティを追加することができる

## 独自メソッド
子クラスには独自のメソッドも定義することができる

## メソッドの呼び出し
子クラスにメソッドが定義されている場合にはそのメソッドが、定義されていない場合には親クラスのメソッドが呼び出される

# instanceof
あるインスタンスが特定のクラスのインスタンスであるかどうか判別することができる<br>
インスタンス instanceof クラス名<br>
if($coffee instanceof Drink);<br>
インスタンスが指定したクラスのインスタンスである場合は「true」に、そうでない場合は「false」

# オーバーライド
同じ名前のメソッドを子クラスで定義するとメソッドの中身を上書きすること<br>

# 子クラスとアクセス権(protected)
子クラスから親クラスで定義したプロパティにアクセスしたい場合は、そのプロパティのアクセス権を「protected」にする<br>
アクセス権がprotectedのプロパティには、そのクラス内からと、そのクラスを継承している子クラス内からのみアクセスすることができる<br>
parent::__construct($name, $price, $image);

# アクセス権まとめ
・public: どこからでもアクセス可能<br>
・protected: そのクラスと子クラス内からのみアクセス可能<br>
・private: そのクラス内からのみアクセス可能

# 重複するコードを1箇所にまとめる(parent)
オーバーライドの際に親クラスで定義したメソッドを呼び出したいとき<br>
parent::メソッド名 <br>
記述した場所で、親クラスのメソッドが実行

# クエリ情報
URLの末尾の「?」以降に「キー名=値」の形で簡単な情報をのせることができる。これをクエリ情報といい、クエリ情報を用いてリンク先のページに情報を渡す（送信する）ことができる<br>
クエリ情報を用いると、show.phpがどのメニューの詳細ページを表示するべきかわかる<br>
echoしないとURLに反映されない<br>
ex)<a href="show.php?name=<?php echo $menu->getName() ?>">

# クエリ情報を受け取る($_GET)
$_GETにはクエリ情報が連想配列として入っている。よって、$_GET['キー名']のように値を取り出せる<br>
ex)$menuName = $_GET['name'] 

# showページの中身
## 特定のインスタンスを取得
$menus = array($curry,$pasta,...)<br>
$menu = Menu::findByName($menus, 'CURRY');

## findByNameメソッドの定義
nameプロパティの値を用いて、配列$menusから特定のMenuインスタンスを取得するクラスメソッド<br>
public static function findByName($menus, $name)<br>
配列$menusの中からnameプロパティが$nameと一致するものを探し、そのインスタンスを戻り値とする

## returnの性質２
戻り値を指定するだけでなく、returnが呼ばれた部分で関数やメソッドの処理を終了させる

 # id
 ## idプロパティの値
 生成されたインスタンスの数を管理し、その数を用いてidプロパティに適した値を入れる<br>
<?php
class User {
  // $idというprivateなプロパティを定義
  private $id;

  // $countクラスプロパティを初期値を数値の0として定義
  private static $count = 0;
  
  public function __construct() {
    // クラスプロパティ$countの値に1を足す
    self::$count++;
    
    // idプロパティにクラスプロパティ$countの値を代入
    $this->id = self::$count;
    
  }
  
  // getIdメソッドを定義
  public function getId() {
    return $this->id;
  }

## idで紐付ける
idを用いてインスタンス紐付けることで確実に特定できる

# インタラクティブ（対話式）モード
php -a

# ウェブサーバー起動
php -s
