# Pythonについて

TODO: ZennとQiitaにまとめたい

## 参考

https://prog-8.com/courses/python

## Pythonの歴史について

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

## コンソールからの入力を受け取る

変数 = input('コンソールに表示したい文字列')」のように使うとコンソールに入力された値が変数に代入される。

inputで受け取った値は文字列型になっているので、数字などの場合は型変換が必要。

```py
input_count = input("個数を入力してください：")
```

## リスト

リストを使って、複数のデータをまとめて管理できる。

```py
fruits = ["apple", "banana", "orange"]
```

リストの値を更新するには以下のように。

```py
fruits[1] = "grape"
```

リストに要素を追加する。
リスト.append(値)により、リストの末尾に値を追加できる。

```py
fruits.append("grape")
```

## 辞書

リストとの違いは、個々の要素をインデックス番号ではなく、「キー」と呼ばれる名前を付けて管理する点。

```py
fruits = {"apple":"りんご", "banana":"バナナ"}
```

値を追加するには以下のように実装する。

```py
fruits["grape"] = 500
```

辞書の繰り返しは以下のように実装する。

```py
fruits = {'apple': 'りんご', 'banana': 'バナナ', 'grape': 'ぶどう'}

for fruit_key in fruits:
    print(fruit_key + "は" + fruits[fruit_key] + "という意味です")
```

## for文

```py
fruits = ['apple', 'banana', 'orange']

for fruit in fruits:
    print("好きな果物は" + fruit + "です")
```

## while文

```py
x = 10
while x > 0:
    print(x)
    x = x - 1
```

## breakとcontinue

breakを使うことで、繰り返し文の中で強制的に処理を終了させることができる。

```py
numbers = [765, 921, 777, 256]
for number in numbers:
    print(number)
    if number == 777:
        break
```

continueはその周の処理だけをスキップすることができる。

```py
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for number in numbers:
    if number % 3 == 0:
        continue
```