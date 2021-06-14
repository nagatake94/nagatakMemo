# 論理型（boolean）

[PHP Docs](https://www.php.net/manual/ja/language.types.boolean.php)

booleanリテラルを指定するには、定数trueまたはfalseを指定する。両方とも大文字小文字に依存しない。

```
<?php
$foo = True; // 値TRUEを$fooに代入する
?>
```

通常、bool 型の値を返す演算子を使用してから、 制御構造にその結果を渡します。

```
<?php
// == は、boolean型を返す演算子
if ($action == "show_version") {
    echo "バージョンは1.23です。";
}

// これは冗長
if ($show_separators == TRUE) {
    echo "<hr>\n";
}

// 上の例は次のように簡単に書くことができます。
if ($show_separators) {
    echo "<hr>\n";
}
?>
```

## booleanへの変換

boolに明示的に変換を行うには、キャスト（bool）または（boolean）を使用する。
しかし、演算子、関数、制御構造がbool型の引数を必要とする場合には、値は自動的に変換されるため、多くの場合はキャストは不要。

### boolに変換する場合、次の値はfalseとみなされる

  - booleanのfalse
  - integerの0
  - floatの0.0及び-0.0
  - 空の文字列、および文字列の"0"
  - 要素の数がゼロである配列
  - 特別な値NULL値（値がセットされていない変数を含む）
  - 属性がない空要素から作成されたSimpleXMLオブジェクト。つまり子要素も属性もない要素

その他はすべてtrue とみなされる

※-1 は、他のゼロでない数と同様に (正負によらず) true とみなされます。

```
<?php
var_dump((bool) "");        // bool(false)
var_dump((bool) 1);         // bool(true)
var_dump((bool) -2);        // bool(true)
var_dump((bool) "foo");     // bool(true)
var_dump((bool) 2.3e5);     // bool(true)
var_dump((bool) array(12)); // bool(true)
var_dump((bool) array());   // bool(false)
var_dump((bool) "false");   // bool(true)
?>
```
