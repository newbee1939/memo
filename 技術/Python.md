# Pythonについて

TODO: ブログにまとめたい

## 参考

https://prog-8.com/courses/python

## 文字列の出力

```py
print("hoge")
```

PHPでいうvar_dump、TSでいうconsole.logみたいな

## 変数

```py
name = "hide"
user_name = "hoge"

# 文字列の連結
hoge = "hide" + "fuga"
```

## 文字と数字のキャスト(変換)

```py
age = 24
print("私は" + str(age) + "歳です")

count = '5'
print(1 + int(count))
```

## if文について

if文の条件式が成立した時の処理を書くときには、インデントを付ける。
処理がif文の中にあるかどうかはインデントによって判別される。
Pythonではコードの見た目（インデント）がそのままプログラムの動作に影響する。

```py
money = 100
apple_price = 100

if money > apple_price:
    print('りんごを買うことができます')
elif money == apple_price:
else:
    print('お金が足りません')
```

## 真偽値

Pythonの真偽値は先頭が大文字。

```py
True
False
```

## andやorやnotで条件式の組み合わせ

```py
x = 20
if 10 <= x <= 30:
    print("xは10以上30以下です")


y = 60
if y < 10 or y > 30:
    print("yは10未満または30より大きいです")


z = 55
if not z == 77:
    print(" zは77ではありません")
```