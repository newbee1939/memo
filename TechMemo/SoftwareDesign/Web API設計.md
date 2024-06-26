## Web APIを美しく設計する重要性

Web APIを美しく設計すべき理由。

- 設計の美しいWeb APIは使いやすい
- 設計の美しいWeb APIは変更しやすい
    - `いきなりAPIの仕様が変わると使っている側が困る`
- 設計の美しいWeb APIは頑強である
- 設計の美しいWeb APIは恥ずかしくない

## Web APIを美しくするには

根幹となる原則。

- 仕様が決まっているものに関しては仕様に従う
- 仕様が存在していないものに関してはデファクトスタンダードに従う

## エンドポイントの基本的な設計

良いURIの設計とは？

`覚えやすく、どんな機能を持つURIなのかがひと目でわかる`

具体的には以下のようなURI。

- 短く入力しやすいURI
- 人間が読んで理解できるURI
    - むやみに省略形を使わない
- 大文字小文字が混在していないURI
- 改造しやすい（Hackableな）URI
    - URIを修正して別のURIにするのが容易である
    - URIを見ただけで使い方が分かるのがベスト
- サーバ側のアーキテクチャが反映されていないURI
- ルールが統一されたURI

## エンドポイント設計の注意点

- `複数形`の名詞を利用する
- 利用する単語に気をつける
- スペースやエンコードを必要とする文字を使わない
- 単語をつなげる必要がある場合はハイフンを利用する

## 検索とクエリパラメータの設計

### 取得数と取得位置のクエリパラメータ

- 以下のいずれか
    - page/per_page
    - offset/limit

offset/limitの方が自由度が高いのでユーザーにとっては使いやすい。

## レスポンスデータの設計

### データフォーマット

- JSONで返す

### データの内部構造

- まず考えるべきことは、`APIのアクセス回数がなるべく減るようにする`

### データはフラットにすべきか？

- `なるべくフラットにすべきだけど、階層化した方が絶対によい場合は階層化もあり`

### 配列とフォーマット

- オブジェクトで包んだ記述方法の方がオススメ

### 各データのフォーマット

- 多くのAPIで同じ意味に利用されている一般的な単語を用いる
- なるべく少ない単語数で表現する
- 複数の単語を連結する場合、その連結方法はAPI全体を通して統一する
- 変な省略形は極力使用しない
- 単数形/複数形に気をつける

### エラーの表現

#### ステータスコードでエラーを表現する

- `適切なステータスコードを使う`

#### エラーの詳細をクライアントに返す

エラーの内容を返す方法は大きく分けて二つある。

- HTTPのレスポンスヘッダに入れて返す方法
- レスポンスボディで返す方法

現実に公開されているAPIはほとんど`ボディにエラーメッセージを格納する方法`を取っている。

#### エラーの詳細情報には何を入れるべきか？

- エラーの詳細コード
    - API提供側で独自にエラーごとに定義したコード
- 詳細情報へのリンク
- メッセージ
    - 開発者向けと非開発者向けを返す方法もある

```json
{
    error: {
        "developerMessage": "hogehoge...",
        "userMessage": "...fugafuga",
        "code": 2013,
        "info": "http://hoge.com",
    }
}
```

#### エラーの際にHTMLが変えることを防ぐ

- エラーの場合にデフォルトでHTMLでエラーを返しているフレームワークやWebサーバーが存在する
- ちゃんとチェックして適切な情報が適切なフォーマットで返るように

#### メンテナンス時

- 503を返す

## 堅牢なWeb APIを作る

### セキュリティの問題のパターン

- サーバとクライアントの間での情報の不正入手
    - `HTTPSにする`
- サーバの脆弱性による情報の不正入手や改ざん
- ブラウザからのアクセスを想定しているAPIにおける問題

### ブラウザ起因の問題

### XSS（クロスサイトスクリプティング）

- `ユーザーの入力を受け取ってそれをページのHTMLに埋め込んで表示する際に、ユーザーから送られたJavaScriptなどを実行できてしまう問題`
    - セッションクッキーなどブラウザに保存された情報にアクセスできる
    - ページの改ざん等も可能
        - やりたい放題...
- APIとしてJSONのようなデータを返す場合でも同様の問題に注意する必要がある
    - e.g. ユーザー名に埋め込まれたJavaScriptが入力のチェックをすり抜けてJSONにも格納されてしまい、それを受け取ったブラウザが画面上に表示 -> JSが実行されてクッキーに含まれたセッション情報が第三者の手に渡ってしまう
- `ユーザーからの入力は必ずチェックする必要がある`
- `データを返す際にも、JSONを返す際にきちんとデータの内容をチェックし、おかしな値を取り除く必要がある`
- JSONなどの形式でデータを返す場合には、上記のようなケース以外にそのデータをブラウザが異なるデータ形式、例えばHTMLであると解釈してしまうために発生してしまうXSSも存在する
    - これを防ぐには、JSONが必ずJSONであるとブラウザに判断してもらえるようにする必要がある
    - `Content-Type`に`application/json`を返すことが重要
    - ただ、これだけだと不十分
    - `X-Content-Type-Options`というレスポンスヘッダを用いる
    - JSとして実行可能なメディアタイプを限定することができ、JSONインジェクションの危険を減らすことができる
    - JSONでデータを返す際には必ず付けるべき

### XSRF（クロスサイトリクエストフォージェリ）

- サイトをまたいで偽装したリクエストを送りつけることで、ユーザーが意図していない処理をサーバに実行させてしまうこと
- XSRFを避ける方法
    - サーバ側のデータが変化するようなアクセスに関しては、GETメソッドを利用せずPOSTやPUT、DELETEなどを用いる
    - XSRFトークンを使う
    - リクエストヘッダの有無で判定する

### JSONハイジャック

- APIからJSONで送られてくる情報を悪意ある第三者が盗み取ること
- SCRIPT要素（<script></script>）に同一生成元ポリシーが適用されないから
- 対策法
    - JSONをSCRIPT要素では埋め込めないようにする
    - JSONをブラウザが必ずJSONと認識するようにする
        - `Content-Type`に`application/json`を返す
    - JSONをJavaScriptとして解釈不可能、あるいは実行時にデータを読み込めないようにする

### ブラウザからのアクセスを想定しないAPIの場合

- なるべくブラウザから簡単に実行されないようにしておく
- SCRIPT要素を利用してURIが貼られてしまった際などに動作しないようにしておく

### 悪意のあるアクセスへの対策を考える

## 参考

- https://www.engilaboo.com/web-api-qa/
- Web API The Good Parts(書籍)
- Google: API 設計ガイド
  - https://cloud.google.com/apis/design?hl=ja
- RESTful Web API の設計
  - https://learn.microsoft.com/ja-jp/azure/architecture/best-practices/api-design
- REST API のベストプラクティス – REST エンドポイント設計の例
  - https://www.freecodecamp.org/japanese/news/rest-api-best-practices-rest-endpoint-design-examples/
- RESTful のウェブ API 設計で避けるべき 6 つのよくあるミス
  - https://cloud.google.com/blog/ja/products/api-management/restful-web-api-design-best-practices/