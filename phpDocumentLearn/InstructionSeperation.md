# 命令の分離

[PHP Docs](https://www.php.net/manual/ja/language.basic-syntax.instruction-separation.php)

C や Perl と同様に、PHP でもステートメントを区切りにはセミコロンが必要と なります。PHP コードブロックの終了タグには自動的にセミコロンが含まれていると 認識されます。 従って PHP コードの最終行にはセミコロンを記述する必要はありません。 ブロックの終了タグは、直後に改行がある場合、それを含んだものになります。

例1 改行を囲んだ終了タグを表示させる例

```
<?php echo "Some text"; ?>
No newline
<?= "But newline now" ?>
```

上の例の出力は以下となります。

```
Some textNo newline
But newline now
```
