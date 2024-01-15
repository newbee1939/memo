# Pythonの基礎を分かりやすくまとめてみた

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

## 関数

```py
def print_hoge():
    print("hogeです")

print_hoge()
```

以下のように引数や初期値を設定することもできる。

```py
def print_hand(hand, name = "ゲスト"):
    print(name + 'は' + hand + 'を出しました')

print_hand("グー")
```

## モジュール

長くなったコードを分割する方法。

「モジュール = Pythonのコードが書かれたファイル」
別ファイルをモジュールとして読み込むことで、そこに書かれたコードを利用することができる。

importを使うことでモジュールを読み込むことができる。
`import モジュール名`の形。モジュール名はファイル名から拡張子（.py）を取り除いたもの

「モジュール名.関数名()」と書くことで、モジュール内の関数を実行することができる。

```py
import utils

utils.print_hand(player_hand, player_name)
```

「from モジュール名 import クラス名」とすることで、そのモジュール内の指定したクラスを直接読み込むことも可能。

```py
from menu_item import MenuItem

menu_item1 = MenuItem('サンドイッチ', 500)
```

## ライブラリ

Pythonには便利なモジュールがいくつか用意されている。
これらのあらかじめ用意されているモジュールは標準ライブラリと呼ばれ、importを用いて読み込むことで便利な関数を利用できるようになる。

- math
- random
- datetime

## passについて

Pythonのpass文は何もしない文であり、文法上なにかを書く必要があるが何も実行することがないときに使う。

## クラス&インスタンス

プログラミングで「もの」を生成するには、まずその「設計図」を用意する必要がある。

設計図のことをクラス、「もの」のことをインスタンスと呼ぶ。

クラスは「class クラス名:」で定義できる。クラス名は大文字から始める。

```py
class MenuItem:
    pass
```

「クラス名()」とそのクラスを呼び出すことで、クラス（設計図）を用いて新しくインスタンスを生成することができる。

```py
menu_item1 = MenuItem()
```

## インスタンスに情報を追加する

インスタンス変数。

```py
class MenuItem:
    pass

menu_item1 = MenuItem()

menu_item1.name = 'サンドイッチ'
print(menu_item1.name)
```

## クラスの中に処理を追加する

クラスの中で定義した関数=メソッド。
メソッドは第1引数にselfを追加する必要がある。

selfには、呼び出したインスタンス自身が代入されている。

クラスの中で定義したメソッドは、インスタンスに対して使うように呼び出す。
具体的には、「インスタンス.メソッド名()」とすることで、そのメソッドを呼び出すことができる。

クラスの中で定義し、インスタンスに対して呼び出すメソッドのことを、「インスタンスメソッド」と呼ぶ。

```py
class MenuItem:
    def info(self):
        print(self.name + ": ¥" + str(self.price))

menu_item1 = MenuItem()
menu_item1.name = 'サンドイッチ'
menu_item1.price = 500

menu_item1.info()
```

## 特殊なインスタンスメソッド

__init__ メソッド

「クラス名()」でインスタンスを生成した直後に自動で呼び出される。

```py
class MenuItem:
    def __init__(self):
        print("MenuItemクラスのインスタンスが生成されました！")

menu_item1 = MenuItem()
```

__init__ を使用することで、インスタンスを生成すると同時にインスタンス変数に値を代入することができる。

```py
class MenuItem:
    def __init__(self):
        self.name = "サンドイッチ"
```

## クラスの継承

あるクラスを元にして新たなクラスをつくること。
「class 新しいクラス名(元となるクラス名):」とすることで他のクラスを継承して、新しいクラスを定義することができる。

```py
from menu_item import MenuItem

class Drink(MenuItem):
    pass
```

## 継承先と継承元のメソッド内の重複

オーバーライドしたメソッドの中で「super()」とすることで、親クラスを呼び出すことができる。

「super().メソッド名()」とすることで、親クラス内に定義されたインスタンスメソッドをそのまま利用することが可能。

```py
from menu_item import MenuItem

class Food(MenuItem):
    def __init__(self, name, price, calorie):
        super().__init__(name, price):
        
        self.calorie = calorie
```

## リンク

- [Pythonの開発環境を用意しよう！（Mac）](https://prog-8.com/docs/python-env)
- [処理の手順を考えよう](https://prog-8.com/docs/python-processing-steps)
- [Pythonを活用しよう](https://prog-8.com/docs/why-learn-python)
