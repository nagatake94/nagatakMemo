# 文字列

[PHP Docs](https://www.php.net/manual/ja/language.types.string.php)

string は、文字が連結されたもの。PHP では、 文字は 1 バイトと同じである。
つまり、256 個の異なる文字を使用可能。
これは、PHP が Unicode をネイティブにサポートしていないことも意味する。

## 構文

文字列リテラルは、4つの異なる方法で指定することが可能である。

  - 引用符
  - 二重引用符
  - ヒアドキュメント構文
  - Nowdoc構文

### 引用符

引用符をリテラルとして指定するには、バックスラッシュ (\) でエスケープする。
バックスラッシュをリテラルとして指定するには、二重 (\\) にする。
それ以外の場面で登場するバックスラッシュは、すべてバックスラッシュそのものとして扱われる。
つまり、\r や \n といったおなじみのエスケープシーケンスを書いても特別な効果は得られず、書いたままの形式で出力される。

※注意: ダブルクォート 構文や heredoc 構文とは異なり、 変数と特殊文字のエスケープシーケンスは、 引用符 (シングルクオート) で括られた文字列にある場合には展開されない。

```
<?php
echo 'this is a simple string';

echo 'You can also have embedded newlines in
strings this way as it is
okay to do';

// 出力: Arnold once said: "I'll be back"
echo 'Arnold once said: "I\'ll be back"';

// 出力: You deleted C:\*.*?
echo 'You deleted C:\\*.*?';

// 出力: You deleted C:\*.*?
echo 'You deleted C:\*.*?';

// 出力: This will not expand: \n a newline
echo 'This will not expand: \n a newline';

// 出力: Variables do not $expand $either
echo 'Variables do not $expand $either';
?>

```

### 二重引用符

記述| 意味   |
|:---|:------------------------|
| \n  | ラインフィード (LF またはアスキーの 0x0A (10))  |
| \r  | キャリッジリターン (CR またはアスキーの 0x0D (13)) |
| \t  | 水平タブ (HT またはアスキーの 0x09 (9))  |
| \v  | 垂直タブ (VT またはアスキーの 0x0B (11))  |
| \e  | エスケープ (ESC あるいはアスキーの 0x1B (27))  |
| \f  | フォームフィード (FF またはアスキーの 0x0C (12))  |
| \\  | バックスラッシュ  |
| \$  | ドル記号  |
| \"  | 二重引用符  |
| \[0-7]{1,3}  | 正規表現にマッチする文字シーケンスは、8 進数表記の 1 文字です。 1 バイトに収まらない部分は、何もメッセージを出さずにオーバーフローする (そのため、"\400" === "\000" となる)。  |
| \x[0-9A-Fa-f]{1,2}  | 正規表現にマッチする文字シーケンスは、16 進数表記の 1 文字 |
| \u{[0-9A-Fa-f]+}  | 正規表現にマッチする文字シーケンスは、Unicode のコードポイントである。 そのコードポイントの UTF-8 表現を文字列として出力する。  |

繰り返しになるが、この他の文字をエスケープしようとした場合には、 バックスラッシュも出力される!

しかし、二重引用符で括られた文字列で最も重要なのは、 変数名が展開されるところである。


### ヒアドキュメント

文字列を区切る別の方法としてヒアドキュメント構文 ("<<<") がある。
この場合、ある ID (と、それに続けて改行文字) を <<< の後に指定し、文字列を置いた後で、同じ ID を括りを閉じるために置く。

終端 ID は、その行の最初のカラムから始める必要がある。
使用するラベルは、PHP の他のラベルと同様の命名規則に従う必要がある。 つまり、英数字およびアンダースコアのみを含み、 数字でない文字またはアンダースコアで始まる必要がある。

※　非常に重要なことだが、終端 ID がある行には、セミコロン (;) 以外の他の文字が含まれていてはならないことに注意。これは、特に ID はインデントしてはならないということ、セミコロンの前に空白やタブを付けてはいけないことを意味する。終端 ID の前の最初の文字は、使用するオペレーティングシステムで定義された 改行である必要があることにも注意を要する。これは、UNIX システムでは macOS を含め \n となる。 最後の区切り文字の後にもまた、改行を入れる必要あり。

この規則が破られて終端 ID が "clean" でない場合、 終端 ID と認識されず、PHP はさらに終端 ID を探し続けます。 適当な終了 ID がみつからない場合、 スクリプトの最終行でパースエラーが発生する。

例1 誤った例
```
<?php
class foo {
    public $bar = <<<EOT
bar
    EOT;
}
// 識別子はインデントしてはいけません
?>
```

例2 有効な例
```
<?php
class foo {
    public $bar = <<<EOT
bar
EOT;
}
?>
```

例3 ヒアドキュメントで文字列を括る例
```
<?php
$str = <<<EOD
Example of string
spanning multiple lines
using heredoc syntax.
EOD;

/* 変数を使用するより複雑な例 */
class foo
{
    var $foo;
    var $bar;

    function __construct()
    {
        $this->foo = 'Foo';
        $this->bar = array('Bar1', 'Bar2', 'Bar3');
    }
}

$foo = new foo();
$name = 'MyName';

echo <<<EOT
My name is "$name". I am printing some $foo->foo.
Now, I am printing some {$foo->bar[1]}.
This should print a capital 'A': \x41
EOT;
?>
```

例3 出力結果
```
My name is "MyName". I am printing some Foo.
Now, I am printing some Bar2.
This should print a capital 'A': A
```

静的な変数やクラスのプロパティ/定数は、 ヒアドキュメント構文で初期化することができる。

例5 ヒアドキュメントを用いた静的な値の初期化
```
<?php
// 静的変数
function foo()
{
    static $bar = <<<LABEL
Nothing in here...
LABEL;
}

// クラスのプロパティ/定数
class foo
{
    const BAR = <<<FOOBAR
Constant example
FOOBAR;

    public $baz = <<<FOOBAR
Property example
FOOBAR;
}
?>
```

### Nowdoc

Nowdoc はヒアドキュメントと似ているが、 ヒアドキュメントがダブルクォートで囲んだ文字列として扱われるのに対して、 Nowdoc はシングルクォートで囲んだ文字列として扱われる。 Nowdoc の使用方法はヒアドキュメントとほぼ同じだが、 その中身について パース処理を行わない。 PHP のコードや大量のテキストを埋め込む際に、 エスケープが不要になる。この機能は、SGML の <![CDATA[ ]]> (ブロック内のテキストをパースしないことを宣言する) と同じようなもの。

Nowdoc の書き方は、ヒアドキュメントと同じように <<< を使用。 しかし、その後に続く識別子をシングルクォートで囲んで <<<'EOT' のようにする。 ヒアドキュメントの識別子に関する決まりがすべて Nowdoc の識別子にも当てはまる。特に終了識別子の書き方に関する決まりに注意。

例7 Nowdoc による文字列のクォートの例

```
<?php
echo <<<'EOD'
Example of string spanning multiple lines
using nowdoc syntax. Backslashes are always treated literally,
e.g. \\ and \'.
EOD;
```

出力結果
```
Example of string spanning multiple lines
using nowdoc syntax. Backslashes are always treated literally,
e.g. \\ and \'.
```
