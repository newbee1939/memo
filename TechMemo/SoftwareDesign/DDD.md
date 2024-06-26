## DDDのコンセプト

- ビジネスの問題を解決するためにビジネスの理解を深め、ビジネスの表現をする
    - ドメインの概念や事象を理解し、その中から問題解決に役立つものを抽出して得られた知識をソフトウェアに反映させる
    - これは、技術指向の開発者であればあるほど疎かにしやすい工程でもある
- `ビジネスとコードを結びつけて、継続的かつ反復的な改良を施せるように枠組みを作る`ことにより、ソフトウェアをより役立つものにしようとする

## DDDとは？

- DDD=ソフトウェアを適用する領域駆動設計
- まず`ドメインモデルを際立たせ`、それがプロジェクトを牽引すべきだとする思想
- コードによるモデリングを中心とし、顧客との反復的な対話を通じて、モデルに表された要求を洗練していくのがDDDの活動
- ものを作るとき、必ず必要になる「知識」が存在する（e.g. 物流システムなら物流の知識など）
- ソフトウェアを作るにあたって必要な知識を取捨選択しつつ、その知識をコードに埋め込むことを実現するのが「ドメイン駆動設計」
- 具体的には、`ドメインについて学ぶ -> ドメインモデルを作り上げる(継続的に改善する) -> ドメインオブジェクトとして実装する`の流れを実践する
    1. ドメインについての理解を深め、モデルを継続的に改善する
    2. モデルを継続的にソフトウェアに反映する

## DDDのコア思想

`みんなでユビキタス言語を使ってドメインエキスパートと話して、ドメイン知識をそのままソフトウェアで表現しろ！`

## ドメインとは？

- ソフトウェアにおける`ドメイン` = `プログラム（ソフトウェア）を適用する対象となる領域`
- ソフトウェアで問題解決しようとする対象領域
    - e.g. メルカリ=フリーマーケット、マネーフォワード=家計簿
    - e.g. 会計システムなら金銭や帳票など

## ドメインモデルとは？

- モデル=現実の事象・あるいは概念を抽象化した概念
- ドメインモデル=モデリングをして得られたモデル
- ドメインの知識を持っているドメインの世界の住人と、開発の知識をもっている開発者は協力（相互補完）しながらドメインモデルを作り上げる必要がある
    - `ドメインモデルを作る作業を開発者だけで完結することは不可能`
    - ドメインの概念に対する捉え方はドメイン実践者の視点が欠かせない
        - ここ中々できないよなあ...
        - 一番大事な気がする

## 良いモデルとは？

- 良いモデル=問題を解決できるモデル
- 問題を解決するには、モデルと実装を正確にマッピングする必要がある
- モデルがコードに正確に反映されていないと、問題を解決することはできない
- そのため、極力`モデルとコードの表現を近づける`ことを目指さないといけない

## 良いモデルを作るには？

- `ドメインエキスパートと会話をする`
    - `これを行わないで開発者の部分的な理解で実装を進めると、徐々に求められているものとの乖離が生じてしまう..`
- 運用して得られた知見をモデルに還元する

## ドメインモデルの作り方

ユースケース図とドメインモデル図を作成する。

### ユースケース図を作成する

- UMLで定義されているもの
- ユーザの要求に対するシステムの振る舞いを定義する図
- アクターとしてユーザーの種類を定義（棒人間のアイコンで定義）し、ユースケースとして「ooをxxする」という形式でシステムの振る舞いを定義（丸い吹き出しで記載）する
- ドメイン図作成のスコープを決める
- どのようなモデルを作るかを判断するための材料として、ユースケースを具体化する
    - ユースケースを具体化することで、モデルが解決すべき問題が明確になる

### ドメインモデル図を作成する

- ドメインモデル図は簡易化したクラス図のようなもの
- 以下のようなルールで記述する
    - オブジェクトの代表的な属性を書くが、メソッドまで書かなくて良い
    - 「ルール/成約(ドメイン知識)」を吹き出しに書き出す
    - オブジェクト同士の関連を示す
    - 多重度を定義する
    - 集約の範囲を定義する
    - 理解を促進するために、具体例などを書いてもいい

## ドメインオブジェクトとは？

- ドメインモデルは、それだけでは何も解決できない
- ソフトウェアとして形にされることで力を発揮する
- ドメインモデルをソフトウェアで動作するモジュールとして表現したのが`ドメインオブジェクト`
- ドメインオブジェクトは`ドメインのコード上の現身`

### ドメインオブジェクトを定義するメリット

- エンティティや値オブジェクトなどのドメインオブジェクトを定義するメリット
    - コードのドキュメント性が高まる
    - ドメインにおける変更をコードに伝えやすくする

### ドメインモデル貧血症とは？

- ドメインモデルを作りながらも、フィールドのGetter/Setterだけをつものを指す
- ドメインオブジェクトに業務知識が実装されず、それを使う側に任されることになる
    - `UseCaseが「何をしたいか(What)」だけでなく、「実装上どのように実現するか(How)」の知識も持ってしまう`
- 同じようなロジックが散在する結果になることが多い
- Active Record型のORマッパーを使った際によく見られる

ドメインモデル貧血症はなぜダメなのか？

- 不整合なデータをいくらでも作れる
    - 全ての属性のセッターがpublicになっているため、他のUseCaseクラスで自由に不整合なデータを作ることができる
- 仕様を追いかけるのに、多くのクラスをコード参照から追う必要がある

## ドメイン層オブジェクト設計の基本方針

- `ドメインモデルの知識を対応するオブジェクトに書く`
- `常に正しいインスタンスしか存在させない`
    - インスタンスをどのタイミングで永続化しても、確実にデータの整合性が保証されるようになる
    - これを実現するには、以下の二つを行う
        - 生成条件の強制
            - 全てのインスタンスはコンストラクタ、もしくはファクトリーメソッドを経由して生成される
            - そのため、存在する生成メソッドが全て正しい条件を強制できれば、新規作成されたインスタンスは全て整合性が保証される
        - ミューテーション条件の強制
            - 全ての項目に対するセッターはx
- `特定のDBやフレームワークには依存させず、層自体を独立させる`
    - 修正しやすさを維持するため

この2つを守ると、保守性の高いコードにすることができる。

## モデル表現を隔離するアーキテクチャ

- 一般的には、モデルの表現以外にも、UIやデータベースとのやりとりといった処理が実装される
- これらの処理とモデルの処理を同じコードの中に混在させると、煩雑で記述量の多いコードになり、可読性、保守性が悪化する
- そこで、モデル表現とその他の処理をレイヤーという単位で大きく分離し、モデル表現を行う層を`ドメイン層`として隔離する

## DDDの用語

二つに大別される。

- モデリング
    - ソフトウェアにとって重要な概念を抽出して抽象化する
- パターン
    - 概念を実装に落とし込む

## DDDの「パターン」の分類について

- ドメインの知識を表現するためのパターン
    - 集約
        - 整合性を保つ境界
        - 値オブジェクトやエンティティといったドメインオブジェクトを束ねて複雑なドメインの概念を表現する
    - 値オブジェクト
        - ドメイン固有の概念（金銭や製造番号など）を値として表現するパターン
    - エンティティ
        - 値オブジェクトと同じくドメインの概念を表現するオブジェクトであるが、値オブジェクトとは対をなすような性質がある
    - ドメインサービス
        - 値オブジェクトやエンティティではうまく表現ができない知識を取り扱うためのパターン
    - 仕様
        - オブジェクトの評価をする
- アプリケーションを実現するためのパターン
    - アプリケーションサービス
        - 値オブジェクト・エンティティ・ドメインサービス・リポジトリの4つの要素を強調させ、アプリケーションとして成り立たせる場がアプリケーションサービス
        - `ユースケース`とも表現される
    - ファクトリ
        - オブジェクトを作る知識に特化したオブジェクト
    - リポジトリ
        - データの保存や復元といった永続化や再構築を担当するオブジェクト
- アプリケーションを実現するためのパターンはドメインの知識を表現するためのパターンを使用する

## 値オブジェクト

- システム固有の`値`を表現するためのオブジェクト
- システムに最適な「値」は必ずしもプリミティブ（単なる変数など、オブジェクトでなく、メソッドを持たないデータのこと）とは限らない
- プリミティブな値は表現力が乏しい
- オブジェクトにした方が適切な場合もある
- DDDでは、このような`システム固有の値`を表現した`オブジェクト`を`値オブジェクト`と呼ぶ
- 値オブジェクトは同一性の判定を`保持する値`で行う

「値」は以下の性質を持っている。そして、「値オブジェクト」にも全く同じ性質が当てはまる。

- 不変である
    - 1という数値がある日突然0になったら..?どう考えても辛い
    - 値は不変であるからこそ、安全に使用できる
    - 値オブジェクトも「値」である以上、値オブジェクトに値を変更するメソッドを定義することは基本的には許されない
        - e.g. Moneyの値オブジェクトでお金の加算をするときも、Addメソッド内でMoneyのオブジェクトを再度生成して返す
    - 不変のメリット
        - 値オブジェクトに限らず、システムを作る上で「不変」には大きなメリットがある
        - `生成したインスタンスをメソッドに渡したら、いつの間にかインスタンスの値や状態が変更されていた`という状況は意図せぬ挙動となりバグを引き起こす

- 交換が可能である
    - 値オブジェクトはそれ自体を変更することはできない
    - 値オブジェクトの変更は代入操作によって行う
```c++
// 以下は値（値オブジェクト）そのものを変更しているので許されない
var fullName = new FullName("taro", "yamada");
fullName.ChangeLastName("sato");

// 以下はOK
var fullName = new FullName("taro", "yamada");
fullName = new FullName("jiro", "yamada");
```

- 等価性によって比較される
    - `0 === 0`の左右の値は、インスタンスとして別のものだが、等価として扱われる
    - 値は値自身ではなく、それを構成する「属性」によって評価される
    - 値オブジェクトも、値オブジェクトを構成する属性（インスタンス変数）によって比較される
値オブジェクトはあくまで「値」なので、以下のように値の属性を取り出して比較するのはおかしい。
```c++
// nameA,Bは値オブジェクト
var compareResult = nameA.FirstName === nameB.FirstName;

// 以下と同じ意味合いになってしまう..
Console.WriteLine(1.value == 0.value);
```
値オブジェクトはあくまで「値」そのものなので、その属性を取り出して比較するのではなく、値と同じようにオブジェクト同士が比較できるようにするのが自然。
そして、このような記述を行うには、値オブジェクト自身が「比較のためのメソッド」を提供する必要がある。
```c++
var compareResult = nameA.Equals(nameB);
```

### 値オブジェクトにする「基準」について

- 値オブジェクトにすべきかの判断基準
    - そこにルールが存在しているか
        - e.g. 氏名には「姓と名で構成される」というルールが存在している
    - それ単体で取り扱いたいか

### 値オブジェクトを採用する理由 

- 表現力を増す
    - 自身の定義により、自分がどういったもの（値）であるかを主張する（自己文書化）
- 不正な値を存在させない
- 誤った代入を防ぐ
    - 単なる文字列ではなく、`UserName`のような値オブジェクトとして表現することで、型の恩恵に与ることができる
- ロジックの散在を防ぐ
    - 例えばユーザーの名前の文字数制限などのロジックを値オブジェクト内に閉じ込めることができる

### 値オブジェクトのサンプルコード

```php
<?php

namespace App\Models\ValueObject;

class ImagePath
{
    private $path;

    public function __construct($filename, $prefix)
    {
        $this->path = 'img.co.jp/hoge/upload/fuga' . '/' . $prefix . '/' . $filename;
    }

    public function dirname()
    {
        return dirname($this->path);
    }

    public function filename()
    {
        return basename($this->path);
    }

    public function path()
    {
        return $this->path;
    }
}
```

```php
<?php

namespace App\ValueObject;

enum PageType
{
    // hoge/fuga/123456/ のようなパス
    case Content;
    // Next.jsの静的ファイル
    case NextStatic;
    // それら以外
    case Other;
}
```

```php
<?php

namespace App\ValueObject;

use App\Parser\UrlParser;

/**
 * ページ種別とそのIDを保持する値
 */
class Page
{
    public readonly string $path;

    /**
     * パースしたページのID、存在しない場合は空文字
     */
    public readonly string $id;

    public readonly PageType $type;

    public function __construct(string $path)
    {
        $this->path = $path;

        $this->type = UrlParser::parseUrlPath($path);

        $this->id = match ($this->type) {
            PageType::Content => (string) UrlParser::getContentId($path),
            default => '',
        };
    }

    /**
     * 記事ページかどうかを判定する
     */
    public function isContent(): bool
    {
        return $this->type === PageType::Content;
    }
}
```

## エンティティ

- 値オブジェクトと対をなすドメインオブジェクト
- 値オブジェクトとの違いは、「同一性によって識別されるか」否か
    - エンティティは同一判定を`識別子`で行う
- 例えば`User`などはその典型
- Userの属性（身長とか名前とか）が変わったからと言って、そのUserが別人になるわけではない
- Userはあくまで「同一性（Identity）」によって区別される
- 逆に「姓名」などは「同一性」ではなく「属性」によって区別される
    - 姓や名が変われば全く別のものになる
    - また、姓名の値が同じであれば同じものとみなされる

- エンティティの性質は以下の通り
    - 可変である
        - 人の身長や体重が変わるように、エンティティの属性は変化することが許されている
            - e.g. Userオブジェクト内のchangeNameメソッドで変更する
            - 値オブジェクトは不変の性質があるため交換（代入）によって変更を表現していたが、エンティティは交換により変更を行わない
            - エンティティの属性を変化させたいときは、その振る舞いを通じて属性を変更する
    - 同じ属性であっても区別される
        - 人間の場合は同姓同名であっても別人として扱われるよね
        - エンティティ同士を区別するためには識別子（Identity）が利用される
            - 識別子は不変にする
    - 同一性により区別される
        - エンティティには同一性を判定するメソッドを追加することが多い（Equalsメソッドなど）
        - 識別子（ID）だけが比較の対象となる

### エンティティにするか値オブジェクトにするかの判断基準

- `ライフサイクル`が存在し、そこに`連続性`が存在するかというのが大きな判断基準
- ユーザーには「作成 -> 属性の変更 -> 削除」などのライフサイクルがある
    - ライフサイクルを持ち、連続性のある概念
- ライフサイクルを持たない、またはシステムにとってライフサイクルを表現することが無意味である場合には、ひとまずは値オブジェクトとして取り扱うと良い

## ドメインサービス

### 概要

- ドメインの概念を知識として落とし込み、それをコードで表現しようとしたとき、`値オブジェクトやエンティティの振る舞いとして定義すると違和感が生じるもの`が存在する
- この違和感は、ドメインのものを表現しようとしたときよりも、ドメインの活動を表現しようとするときに見られる傾向がある
- 違和感のある振る舞いを値オブジェクトなどに無理やり実装しようとすると、オブジェクトの責務を歪なものに変えてしまう
- このようなときに求められることは、その振る舞いを別のオブジェクトとして定義すること
- ドメインサービスはまさにそのオブジェクト

### サービスとは？

- ソフトウェアの文脈における「サービス」は`クライアントのために何かを行うオブジェクト`
- ドメイン駆動設計における「サービス」は以下の二つ
    - ドメインサービス
        - ドメインのためのサービス
        - ドメインにおける活動
        - 矢印がドメインに向いている
    - アプリケーションサービス
        - アプリケーションのためのサービス
        - アプリケーションとして成り立たせるためのサービス
        - 矢印がアプリケーションに向いている
- ドメインオブジェクトは自身のためのふるまいを持っているが、サービスは自身のためのふるまいは持っていない
    - サービスはものごとではなく、活動や行動であることが多い

### ドメインサービスとは？

- 例えば、Userオブジェクトの同姓同名を許容しないアプリケーションがあって、同姓同名のUserが既に存在しているかどうかをチェックしたい場合、そのチェックの処理をどこに記述するか？
- Userクラスに定義するのは`違和感`がある
    - Userオブジェクト自身に他に重複するユーザーがあるかどうかを聞く？
- こういった`不自然`で`違和感`のある振る舞いを記述するために使用するのが「ドメインサービス」
- 例えば複数のドメインオブジェクトを横断するような操作など
- 以下のように記述する
```java
class UserService
{
    public bool Exists(User user)
    {
        // 重複確認
        // ...
    }
}
```
- ドメインサービスは、値オブジェクトやエンティティと異なり、自身のふるまいを変更するようなインスタンス特有の状態を持たないオブジェクト
- ここで大事なのは、ドメインサービスに実装するのは、`ドメインオブジェクトに実装すると違和感があるもの`に限定すること
- そうしないと、あらゆる処理がドメインサービスに実装されていってしまう
    - `ドメインモデル貧血症`（ドメインオブジェクトに記述されるべき知識や振る舞いがドメインサービス等に記述され、語るべきことを何も語っていないオブジェクトの状態）を招く
- `迷ったらドメインオブジェクトに実装`する
- なるべくドメインサービスには実装しない

### ドメインサービスの命名規則について

- ドメインサービスの命名規則は主に3パターン
    - ドメインの概念
    - ドメインの概念 + サービス
    - ドメインの概念 + DomainService
- サービスはドメインの活動がその対象となりやすく、動詞に基づいて命名されることが多い

## リポジトリ

- リポジトリ=データの保管庫
- 集約単位で永続化層へのアクセスを提供するもの
- 永続化層との入出力
- リポジトリはデータにまつわる処理を分離する
- そして、永続化や再構築（データの取得）を担う
- データの永続化や再構築等の処理をドメインサービスからリポジトリの切り出すことで、ドメインサービスの役割がよりはっきりする（無駄に長い永続化や再構築の処理が抽象化されるので）
    - ドメインオブジェクトを際立たせることができる
- さらに、データストアにまつわる処理を切り出すことで、データストアの差し替えも容易にすることができる
    - `インターフェース`をうまく活用することで、より差し替えを容易にできる
- リポジトリ内の処理は、SQLを直接記述するだけでなく、ORMを使って記述することもできる
- リポジトリは`Listのように扱う`のがポイント
    - ドメイン知識は持たない

### リポジトリに定義する振る舞い

リポジトリでは、以下のように更新項目を引き渡す更新処理は行わない。
リポジトリに多くの更新処理を定義させる結果に繋がってしまうので。。

```java
interface IUserRepository
{
    void UpdateName(UserId id, UserName name)
    ...
}
```

永続化のふるまいは永続化を行うオブジェクトを引数に取るようにする。
オブジェクトが保持するデータを更新するなら、ドメインオブジェクト自身に依頼すべき。

```java
interface IUserRepository
{
    void Save(User user)
    ...
}
```

同様にオブジェクトを生成する処理もリポジトリには定義しない。
データの破棄の処理はリポジトリに実装する。

再構築の振る舞いは識別によって検索されるメソッドで、以下のように記述する。

```java
interface IUserRepository
{
    User Find(UserId id);
    ...
}
```

### リポジトリの実装場所について

- ドメインオブジェクトがリポジトリを受け取る場合について
- これはあまり良くない
- リポジトリはドメイン設計を完成させる意味ではドメインのオブジェクトである
- しかし、`ドメイン由来`のものではない
- ドメインモデルの表現に徹することができていない
- エンティティや値オブジェクトがドメインモデルの表現に徹するためには、リポジトリを操作することを可能な限り避ける必要がある
    - Eloquent等でDB操作するのも避けた方がよさそう

### 外部APIとリポジトリの関係

- `外部APIに渡す値、外部APIから取得する値が、ドメインモデルとして意味を持つのであれば、ドメイン層のものとして定義してリポジトリで設計する`

### 一部カラムを更新するときの扱い

- エンティティの一部分だけの更新をしたい場合、一部分だけリポジトリに渡すのではなく、エンティティを丸ごと渡して丸ごと更新する必要がある
- リポジトリは必ず集約単位で更新処理を行う

### ドメインオブジェクトからリポジトリ操作の可否

- ユースケースからではなく、エンティティからリポジトリを利用してDBからの取得や更新などの操作をしてもいいのか？
- エンティティが複数の責務を持つことになるので非推奨
- 責務が増えると凝集度が下がり、可読性や保守性を下げる

### ORマッパーとドメイン層の関係性について

- 代表的なのは、Active Record型の、テーブルと対応したクラス
- `これらのクラスをドメイン層のクラスとしてそのまま使ってはいけない`
- そのまま使うと、以下のようなデメリットがある
    - 全ての項目にセッターがあるため、更新処理に制限をかけられなくなる
    - テーブルとオブジェクトが切り離せなくなるため、オブジェクトとテーブルの設計に望ましくない制約がかかってしまう
- そのため、`Active Record型のテーブルに対応したクラスはインフラ層のリポジトリ実装クラス内に閉じ込め`、`DBデータを取得した結果をドメイン層のクラスに詰め替える`形にする
- こうすることで、`ドメイン層、ユースケース層が特定のORマッパーの知識を持たないように`隠蔽できる

## アプリケーションサービス

### 概要

- 端的に言うと、`ユースケースを実現するオブジェクト`
- アプリケーションサービスはドメインオブジェクトを強調させてユースケースを実現する
- 値オブジェクトやエンティティといったドメインオブジェクトはドメインモデルをコードによって表現したオブジェクト
- ソフトウェアとして利用者の問題を解決するには、これらのドメインオブジェクトをまとめあげて問題を解決するように導く必要がある
- アプリケーションサービスはドメインオブジェクトが行うタスクの進行を管理し、問題の解決に導く

### アプリケーションサービスでドメインオブジェクトの取得をする場合

- ドメインオブジェクトをクライアントにそのまま返すべきか？
- アプリケーションサービス以外のオブジェクトがドメインオブジェクトの直接のクライアントとなって自由に操作できてしまうのは問題
- ドメインオブジェクトの振る舞いを呼び出すのはアプリケーションサービスの役割
- その枠組みを越えてドメインオブジェクトの振る舞いが呼び出されてしまうと、本来であればアプリケーションサービスとして提供されるべきであったコードが各所に散りばめられてしまう
- また、ドメインオブジェクトに対する依存が多く生まれるのも問題
- ドメインオブジェクトを変更しづらくなる
- ドメインの変更をドメインオブジェクトに反映させるスピードが落ちる
- そこでおすすめなのが、ドメインオブジェクトを直接公開しない方法
- ドメインオブジェクトを非公開としたとき、クライアントには`データ転送用オブジェクト（DTO, Data Transfer Object）`にデータを移し替えて返却する
- これにより、クライアントはドメインオブジェクトのメソッドを呼び出せなくなる（ドメインオブジェクトの操作ができなくなる）
- 以下に具合例を示す

```java
// DTO
public class UserData
{
    public UserData(string id, string name)
    {
        Id = id;
        Name = name;
        
        public string Id { get; }
        public string Name { get; }
    }
}
```

```java
public class UserApplicationService
{
    private readOnly IUserRepository userRepository;

    public UserData Get(string userId)
    {
        var targetId = new UserId(userId);
        var user = userRepository.Find(targetId);

        // DTOに詰め替える
        var userData = new UserData(user.Id.Value, user.Name.Value);
        return userData;
    }
}
```

### アプリケーションサービスの役割について

- アプリケーションサービスはあくまでドメインオブジェクトの操作や調整に徹するべき 
- アプリケーションサービス内にドメインのルールは記述されるべきではない
- アプリケーションサービス内にドメインのルールは記述すると、様々なファイルに同じようなロジックが点在する事態になってしまう可能性がある
- ドメインのルールはドメインオブジェクトに実装する
- 具体的には、ドメインオブジェクトの生成や状態の変更、リポジトリを用いた永続化などを行う

### アプリケーションサービスの分割について

classの凝集度を高めるために、以下のようにファイルを分割するパターンも多い。

- Application
    - Users
        - UserRegisterService
        - UserGetInfoService
        - UserUpdateInfoService
        - UserDeleteService

また、アプリケーションサービスはインターフェースを通すことも多い。

### サービスは状態を持たない

- アプリケーションサービスが状態（インスタンス変数など）を持ってしまうと、クライアント側がアプリケーションサービスの状態を気にしなくてはならなくなる
- 状態がもたらす複雑さは多くの開発者を混乱させる

### ユースケースについてとアプリケーションサービスの違いについて

- 基本的には`アプリケーションサービス=ユースケース`
- アプリケーションサービスだと何をする場所なのかが分かりづらい
- ユースケースの方が責務が明確になる
- そのため、ファイル名も`ApplicationService`ではなく、`UseCase`とする方が分かりやすい気もする

### ユースケースクラスの分割単位

- `1クラスに1パブリックメソッド`にするのが良さそう

### CQRS（コマンドクエリ責務分離）

- レイヤーとしては`ユースケース層`に定義する内容
- DDDでは、永続化層との入出力はリポジトリを使う
- 更新系の処理では、`エンティティや値オブジェクトでドメイン知識を表現`し、`リポジトリを使って集約単位で永続化する`という構成を取ると、非常に保守性のいいものになる
- しかし、参照系の処理、特に一覧画面で複数の集約の情報を表示したいような画面で、リポジトリを使用するだけだと問題が発生することがある
    - e.g. タスク、ユーザー、ラベルという3つの集約があり、それぞれにリポジトリがある場合
- これを1つのユースケースクラスで実現すると、3つのリポジトリからそれぞれ値を取得し、戻り値のクラスに詰め替えるような実装にせざるを得ない
- すると、以下のような問題が発生する
    - 複数の集約から値を取得して戻り値の型に詰め替える処理が、ループが増えて読みにくいコードになる
    - 画面に返す必要のない値を取得するのでパフォーマンスが悪化する
    - 複数集約の条件で絞り込んでのページングができない
- そこで、`CQRS`を導入する
- CQRS = `参照に使用するモデルと更新に使用するモデルを分離する`アーキテクチャ
- `更新系のクエリと参照系のクエリを分ける`ということ
- 更新系モデルは、ドメインオブジェクト（エンティティ、値オブジェクト）をそのまま使用する
- 参照系モデルは、`特定のユースケースに特化した値の型`（DTO）を定義する
    - また、その値を取得するためのサービス（クエリサービス）も独自に定義する

## 依存関係のコントロール

### 概要

- ソフトウェアに柔軟性をもたらすために必要なことは「依存関係を制御」すること
- 依存関係を軽視すると、ソフトウェアは途端に柔軟性を失う
- ソフトウェアを柔軟に保つために必要なことは、特定の技術要素への依存を避け、変更の主導権を`抽象`に移すこと
- 重要なのは、依存を「避ける」のではなく、「コントロール」すること

### 依存性逆転の法則について

以下のアプリケーションサービスとリポジトリについて、アプリケーションがリポジトリで使用されている特定の技術基盤に依存しているのは問題である。

```
UserApplicationService -----> UserRepository
```

そこでUserRepositoryのインターフェースを用意する。（IUserRepository）
アプリケーションサービスはリポジトリを直接見るのではなく、インターフェースを参照するようにする。

```
UserApplicationService -----> IUserRepository <----- UserRepository
```

もともと具体的な実装に依存していたものが抽象に依存するように、`依存関係は逆転`した。

これにより、アプリケーションサービスが特定の技術に依存しているリポジトリに直接依存することはなくなる。

抽象型（インターフェース）を利用すると、具象型に向いていた依存の矢印が抽象型へ向くようになる。
このように依存の方向性を制御し、全てのモジュールが抽象へ依存するように制御することは、ビジネスロジックを具体的な実装から解き放ち、より純粋なものに昇華する効果がある。

この抽象型を用いた依存関係の制御は「依存関係逆転の原則（Dependency Inversion Principle）」として知られている。

### 依存関係逆転の原則とは？

DIPは以下のように定義されている。

- 上位レベルのモジュールは下位モジュールに依存してはならない、どちらのモジュールも抽象に依存すべきである
- 抽象は、実装の詳細に依存してはならない。実装の詳細が抽象に依存すべきである

### 依存関係をコントロールする

以下のように実装してしまうと、あらゆる箇所でリポジトリの種類を切り替える必要がある。

```java
public class UserApplicationService
{
    private readonly IUserRepository userRepository;

    public UserApplicationsService()
    {
        // this.userRepository = new InMemoryUserRepository(); <----ここを切り替える必要がある
        this.userRepository = new UserRepository();
    }
    
    ...
}
```

そこで利用できるのが以下の二つのパターン。

- Service Locatorパターン
- IoC Containerパターン

#### Service Locatorパターンについて

ServiceLocatorと呼ばれるオブジェクトに依存解決先となるオブジェクトを事前に登録しておき、インスタンスが必要となる各所でServiceLocatorを経由してインスタンスを取得するパターン。

```java
public class UserApplicationService
{
    private readonly IUserRepository userRepository;

    public UserApplicationService()
    {
        // ServiceLocator経由でインスタンスを取得する
        this.userRepository = ServiceLocator.Resolve<IUserRepository>();
    }
    
    ...
}
```

これにより、ServiceLocatorの登録を切り替えるだけで、簡単にインスタンスを差し替えることができる。

一方でService Locatorパターンは以下の理由からアンチパターンであるとも言われている。

- 依存関係が外部から見えづらくなる
    - 「ApplicationServiceを動作させるために事前にServiceLocatorに対して依存解決の設定を行う必要がある」のが、クラス定義を見ただけでは分からないのが辛い
- テストの維持が難しくなる

#### IoC Container（DI Container）パターン

まずはDI（Dependency Injection）について。
DIは`依存の注入`という言葉で訳される。

以下は、依存を注入している例。

```java
var userRepository = new InMemoryUserRepository();
var userApplicationService = new UserApplicationService(userRepository);
```

上記の場合は、コンストラクタで依存するオブジェクトを注入しているので`コンストラクタインジェクション`とも呼ばれる。
DIパターンにはこれ以外にメソッドで注入するメソッドインジェクションなど多くのパターンが存在する。

DIパターンであれば依存関係の変更に強制力を持たせられる。

例えば、以下のようにUserApplicationServiceに新たな依存関係を追加してみる。

```java
public class UserApplicationService
{
    private readonly IUserRepository userRepository;
    // 新たにIFooRepositoryへの依存関係を追加する
    private readonly IFooRepository fooRepository;

    // コンストラクタで依存を注入できるようにする
    public UserApplicationService(IUserRepository userRepository, IFooRepository fooRepository)
    {
        this.userRepository = userRepository;
        this.fooRepository = fooRepository;
    }
    ...
}
```

これにより、UserApplicationServiceをインスタンス化して実施しているテストはコンパイルエラーにより実行できなくなる。
テストを実施するために開発者はコンパイルエラーを解消することを余儀なくされる。これは大きい強制力。

しかし、これだと、依存するオブジェクトのインスタンス化をあちこちに記述する必要が出てきてしまう。

この問題を解決するために活躍するのがIoC Containerパターン。

```java
// IoC Container
var serviceCollection = new ServiceCollection();
// 依存解決の設定を登録する
serviceCollection.AddTransient<IUserRepository, InMemoryUserRepository>();
serviceCollection.AddTransient<UserApplicationService>();

// インスタンスはIoC Container経由で取得する
var provider = serviceCollection.BuildServiceProvider();
var userApplicationService = provider.GetService<UserApplicationService>();
```

## ファクトリ

### 概要

- オブジェクトの生成はときに複雑な手順を必要とする
    - 本来は初期化はコンストラクタの役割
    - しかし、コンストラクタは単純である必要がある
    - コンストラクタが単純でなくなるときにはファクトリを定義する
- そういった手順は、モデルを実現するオブジェクトに無理やり実装するよりも、オブジェクトの生成それ事態を独立したオブジェクトとする方がコードの意図を明確にすることに繋がる
- 道具を作ることと道具を使うことは全く別の知識であるのと同様に、オブジェクト生成の責務はモデルを表現するオブジェクトにはふさわしくない
- ファクトリはオブジェクトの生成方法に関する知識がまとめられたオブジェクト

## 集約

- 集約=変更の単位
- 必ず守りたい`強い整合性を持った`オブジェクトのまとまり
- データを変更するための単位として扱われるオブジェクトの集まりを集約と言う
- 集約にはルートとなるオブジェクト（集約ルート）が存在し、全ての操作はルート越しに行われる
- 集約は不変条件を維持する単位として切り出され、オブジェクトの操作に秩序をもたらす
- 集約には`境界`と`ルート`が存在する
    - 集約の`境界`は集約に何が含まれるのかを定義するための境界
    - 集約のルートは集約に含まれる特定のオブジェクト
- Userエンティティなどのオブジェクトは`集約`にあたる
- 一つの集約のオブジェクトは、必ず集約単位でリポジトリから取得し、集約単位でリポジトリに渡す
    - 1トランザクションで集約内の全てのオブジェクトを更新する
    - 集約の中の一部オブジェクトのみの取得/更新は許可しない
        - 集約内のオブジェクトの整合性が崩れるのを防ぐため
        - e.g. 部と部員の数と承認状態の関係性など

### 集約の境界の決め方

次の二つの観点を考慮して決定する。

- 整合性を確保する必要性の強さ
    - 整合性を`強く`確保したいものを一つの集約にする
- トランザクション範囲の適切さ
    - 集約の範囲を大きくしすぎるとデータベースに対して不必要に大きなロックを取り、問題が発生する

### 集約の基本的構造

- 集約の外部から境界の内部オブジェクトを操作してはならない
- 例えば、以下でUserNameを直接操作して良いのは集約ルートであるUserのみ
- ユーザー名の変更はUserオブジェクトに依頼をする形で変更をしなくてはいけない

```java
var userName = new UserName("NewName");

// NG
user.Name = useName;

// OK
user.ChangeName(userName);
```

- changeNameといったメソッドを用意することで引き渡された値の確認を行える
    - 不正な値を防げる
- オブジェクト指向プログラミングではこのように、外部から内部のオブジェクトに対して直接操作するのではなく、それを保持するオブジェクトに依頼する形を取る
- そうすることで、直感的に、かつ不変条件を維持することができる
    - これは`デリメルの法則`としても知られる

## 仕様

- `仕様`はオブジェクトの`評価`を行うオブジェクト
- オブジェクトの評価はときに`複雑な手順`が必要になる
- こうした評価処理をオブジェクトのメソッドとして定義すると、オブジェクト本来の趣旨を見えづらくしてしまうことがある
- また、こうした複雑な評価の手順は、アプリケーションサービスに記述されてしまうことも多い
- しかし、オブジェクトの評価はドメインの重要なルールであるため、サービスに記述されてしまうことは問題
- そこで、評価処理はオブジェクトに定義する以外に、評価自体をオブジェクトとして切り出すことが可能
- そうして切り出された条件に合致しているかどうかを見極めるオブジェクトが`仕様`

### 複雑な評価処理を確認する

あるオブジェクトが特定の条件にしたがっているかを評価する処理は、オブジェクトのメソッドとして定義される。

たとえば、以下のようなドメインオブジェクトにも評価を行うメソッドが存在している。

```java
public class Circle
{
    public bool IsFull()
    {
        return CountMembers() >= 30;
    }
}
```

このくらい単純であれば問題はない。しかし、これよりも複雑であった場合はどうか？

こういう場合に、`仕様`として評価処理をオブジェクトに切り出すことができる。

これにより、値オブジェクトやエンティティにリポジトリを操作させないことも実現できる。

### 趣旨が見えづらいオブジェクト

オブジェクトの評価処理を安直にオブジェクト自身に実装すると、オブジェクトの趣旨がボヤける。
オブジェクトが何のために存在し、何を為すのかが見えづらくなる。

```java
public class Circle
{
    public bool IsFull();
    public bool IsPopular();
    public bool IsLocked();
    ...
}
```

オブジェクトを評価する方法はメソッドに限ったことではない。
仕様のように外部のオブジェクトとして切り出すことも可能であると覚えておく。

## ドメイン駆動設計とアーキテクチャの関係性(ドメイン駆動設計がアーキテクチャに求めること)

- 開発者が`利口なUI`等の設計におけるアンチパターンを避けるには、`自制心`は心許ない
- そこで利用するのが`アーキテクチャ`
- アーキテクチャがあることで、開発者は「どこに何を記述するか」に振り回されることがなくなる
- DDDの本質である「ドメインを捉え、うまく表現する」ことに集中することができる
- つまり、`アーキテクチャはDDDに集中するための助けになる`ということ
- アーキテクチャを取り入れることで、ドメインの本質に集中する環境を用意することができる

## 軽量DDDに陥らないために

### 軽量DDDとは？

- `軽量DDD`
    - `ドメイン駆動設計に登場するパターンだけを取り入れる手法`
    - e.g. エンティティ、リポジトリ、、など
- 軽量DDDはコードの書き方を主題としているので、開発者だけで完結させることが可能で実践しやすく、短期的にプロダクトのコードにある程度の秩序をもたらす
- しかし、ドメイン駆動設計が目指すことは、決してパターンに終始することではない
- パターンを主軸にすることは、全ての問題に技術的な解決を求めるのと何ら変わりない
- もっとも重要なことは`ドメインの本質に向き合う`こと
- 技術的なパターンは絶対的な答えとして君臨するものではなく、ドメインの本質に向き合い、それをうまくコード上で表現するためのサポート役として機能する

### ドメインエキスパートとモデリングする

- 開発者は`ドメインエキスパート`と呼ばれるドメインの精通者たちと会話をしなくてはならない
- ドメインの問題を解決するソフトウェアを開発するにあたって、ドメインと向き合うことは避けられない

### ユビキタス言語

#### 説明1

- `発見したモデルの言葉を、全ての場所で使う`という指針
- `ユビキタス`の意味=`In Everywhere`
- 開発者だけでなく、ビジネス側の人も同じ言葉を使うことはもちろん、「会話でも、ドキュメントでも、コードでも」ということを意味する
- 場所によって違う言葉が使われると、言い換えや変換が行われる
- 言葉が変換される際、意味の損失や認識ずれがどうしても発生する
- どこでも同じ言葉を使うことで、言葉の変換を極力無くすことを目指す

#### 説明2

- プロジェクトには認識の齟齬や翻訳にコストをかけないためにも共通言語を作ることが求められる
- そのようなプロジェクトにおける共通言語のことを`ユビキタス言語`という

### 境界付けられたコンテキスト

- 基本的には「1コンテキスト1アプリケーション」が良さそう
- それが難しい場合はパッケージ（ディレクトリ）で分割するなど
    - 後からアプリケーション分割しやすい形に

#### 説明1

- `境界付けられたコンテキスト`はドメインの国境のようなもの
- 国の境を越えると扱う言語が異なるようにドメインにも境が存在し、その境を越えるとユビキタス言語が変わることがある

#### 説明2

- あるモデルを、同じ意味で使い続ける範囲を定義するもの
- そうすることにより、モデルを適切な粒度に分割し、精度を上げることを目指す

#### 説明3

- 特定のモデルを定義・適用する境界を明示的に示したもの
- 代表的な境界の例はサブシステムやチームなど
- システムが大規模になると、関係者全てで統一したモデルを作ることは難しくなる
    - e.g. 「経理」「配送」「企画」のそれぞれで「商品」に対するイメージは異なる
- そこで、DDDでは、モデルが適用される範囲を明示的に定義し、それぞれの中でモデル言語の統一を目指す
- この明示的に定義された範囲を`境界づけられたコンテキスト`と呼ぶ
    - e.g. 「販売コンテキスト」「配送コンテキスト」など

## MVCのModelとは？エンティティとの違いは？

https://allabout-tech.hatenablog.com/entry/2016/11/29/100000

## プレゼンテーション層

要は、コントローラのこと

### レスポンス仕様の定義

- プレゼンテーション層ではレスポンスの仕様を定義する
- HTMLレンダリングを行うコントローラの場合、UIにまつわるもの（色、文字の書式など）を決めるのもプレゼンテーション層の責務
- ユースケース層やドメイン層のオブジェクトが、保持する値を表示用にフォーマットするメソッドを持っていたら、それは責務違反
    - 凝集度が下がり、結果として可読性、保守性を下げる

### プレゼンテーション層における値オブジェクトの生成

- コントローラで値オブジェクトを生成してもいいのか？
    - ドメインオブジェクトの公開されたメソッドを組み合わせてユースケースを実現するのは、ユースケース層の責務
    - そのため、値オブジェクトの生成を行うのはユースケース層に寄せる方が適切

## 戦略的設計と戦術的設計

- DDD に登場する概念は大きく`戦略的設計`と`戦術的設計`に分かれる
- 戦略的設計は`思想`と`システムの分割・結合`の話、戦術的設計は`レイヤー構成`と`ビジネスロジックの実装方法`の話に分かれる
- 戦略的設計
    - ドメインモデリングの前提を揃えるための、モデリング対象を定義する原則と手法(コアドメイン/サブドメイン、境界付けられたコンテキスト、コンテキストマップ等)
- 戦術的設計
    - モデルを具体的に表現するためのパターン(エンティティ、レポジトリ、レイヤードアーキテクチャ等)
- 戦略的設計は、具体的な細かいテクニックである戦術的設計よりも大局的な話
- 戦術的設計だけを使うことを`軽量DDD`と呼ぶことが多い

## DDD参考書籍

- [ドメイン駆動設計入門 ボトムアップでわかる！ドメイン駆動設計の基本](https://www.shoeisha.co.jp/book/detail/9784798150727)
- ドメイン駆動設計 モデリング/実装ガイド
- [ドメイン駆動設計 サンプルコード&FAQ](https://little-hands.booth.pm/items/3363104)

## DDD買いたい本

- ドメイン駆動設計をはじめよう ―ソフトウェアの実装と事業戦略を結びつける実践技法
    - https://amzn.asia/d/023jiz2o
- ［入門］ドメイン駆動設計――基礎と実践・クリーンアーキテクチャ (Software Design別冊)
    - https://amzn.asia/d/02aJcv3J
- 関数型ドメインモデリング ドメイン駆動設計とF#でソフトウェアの複雑さに立ち向かおう
    - https://amzn.asia/d/06Mn3kuL

## DDD参考リンク

- [【DDD入門】TypeScript × ドメイン駆動設計ハンズオン](https://zenn.dev/yamachan0625/books/ddd-hands-on)
- [DDDはなぜ難しいのか / 良いコードの定義と設計能力の壁](https://speakerdeck.com/pospome/liang-ikodonoding-yi-toshe-ji-neng-li-nobi)
- [little hands' lab](https://little-hands.hatenablog.com/)
- [DDD はオブジェクト指向を利用してどのようにメンテナブルなコードを書くか](https://little-hands.hatenablog.com/entry/2020/02/17/ooc)
- [第一回 DDD 勉強会を開催しました！](https://note.com/loglass_sakamoto/n/n7472f7df0892)
- [モデリングについての質問](https://querie.me/answer/x3z4F7mrW2vUZ5sOFD3S?timestamp=1712668675)
- [DIについて](https://qiita.com/okazuki/items/a0f2fb0a63ca88340ff6)
- [なぜDDD初心者はググり出してすぐに心がくじけてしまうのか](https://little-hands.hatenablog.com/entry/2017/09/24/005903#google_vignette)
- [CQRS実践入門 [ドメイン駆動設計]](https://little-hands.hatenablog.com/entry/2019/12/02/cqrs)
- [DDDのQ&A](https://querie.me/user/little_hand_s)
- [DDDのQ&Aのアーカイブ](https://github.com/little-hands/ddd-q-and-a?tab=readme-ov-file)

## TODO

- DDDイラストの完成と定期的な更新
    - https://www.canva.com/design/DAGA94WP2ZI/G_UA4aBkxDcCknudtHvz_w/edit
    - 再度このページを読み返しつつ
- PHPでの値オブジェクトの書き方のサンプル
- TODO: このメモをより分かりやすく整理する