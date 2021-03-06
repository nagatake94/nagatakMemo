# HTMLからの脱出

[PHP Docs](https://www.php.net/manual/ja/language.basic-syntax.phpmode.php)


PHP のパーサは、開始タグと終了タグに囲まれていない部分をすべて無視します。 そのおかげで、PHP のファイルにそれ以外のコンテンツを混在させることができるのです。 たとえば PHP を HTML ドキュメントに組み込んで、テンプレートを作ったりすることもできます。

```
<p>この部分は PHP から無視され、そのままブラウザには表示されます。</p>
<?php echo '一方、この部分はパースされます。'; ?>
<p>この部分も PHP から無視され、そのままブラウザには表示されます。</p>
```

これは期待通りに動作します。なぜなら、PHP インタプリタは ?> 終了タグを見つけると それ以降新たに開始タグを見つけるまでの内容を何でも出力するからです (終了タグの直後の改行は別です。 命令の分離 を参照ください)。 しかし、PHP が条件文の中にいる場合は話が別です。 その場合は、まず条件式の結果を判定してから何をスキップするかを判断します。 次の例を参照ください。
条件文を使った例です。

```
<?php if ($expression == true): ?>
  条件式が真の場合にこれが表示されます。
<?php else: ?>
  それ以外の場合にこちらが表示されます。
<?php endif; ?>
```
