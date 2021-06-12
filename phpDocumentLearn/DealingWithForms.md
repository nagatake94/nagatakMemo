# フォームの処理

[PHP Docs](https://www.php.net/manual/ja/tutorial.forms.php)

PHPの最も強力な機能の一つは、HTMLフォームを処理する手段である。理解するべき重要な基本概念は、あるフォームの中のすべての要素が、自動的にPHPスクリプトで利用可能になる

例1 簡単なHTMLフォーム

```
<form action="action.php" method="post">
 名前: <input type="text" name="name" />
 年齢: <input type="text" name="age" />https://www.php.net/manual/ja/tutorial.forms.php
 <input type="submit" />
</form>
```

このフォームに関して特別なところはない。
ユーザーがこのフォームを記入し、投稿ボタンを押した時、action.phpページが呼ばれる。
このファイルには、以下のようなコードを記述する。

例２ フォームからのデータを出力する

```
こんにちは、<?php echo htmlspecialchars($_POST['name']); ?>さん。
あなたは、<?php echo (int)$_POST['age']; ?> 歳です。
```

出力結果は以下の通り

```
こんにちは、nagatak さん。あなたは、24 歳です。
```

## htmlspecialchars()及び数値変換

htmlspecialchars() および (int) の部分以外は、何を行っているかは明らかでしょう。 htmlspecialchars() は、html での特殊な文字を適切にエンコードし、 HTML タグや Javascript をページ内に仕込めないようにします。 また、age フィールドには数値が入ることがわかっているので、これを int 型に 変換 します。これにより、おかしな文字が入力されることを防ぎます。
