## ReferenceError

「参照エラー」のこと。
存在しない変数を参照しようとして発生する。
↓
変数が正しく定義されているかを確認すればよい

## TypeError

プログラム中の値を不適切な方法で扱った場合に発生するエラー。

## Uncaught Error

`try-catch`によって処理されなかったエラー

## スタックトレース

処理の流れとエラーの発生場所を教えてくれる。

- stack: 山積みにされたもの
- trace: 足跡/記録

`sample.html:10:7`とあれば、sample.htmlの10行目の7列目（行の先頭から7文字目）でエラーが発生したことが分かる。

VSCode上で`sample.html:10:7`と入力すればその場所に移動できる。

## デバッグの方法

### プリントデバッグ

`console.log`とかで変数の中身を確認しつつデバッグすること。

そもそも処理自体が呼ばれているかを確認する際にも使える。

### 二分探索

範囲が広い場合は、闇雲にプリントデバッグするのではなく、全体を見渡して原因となりそうな箇所を少しずつ絞り込んでいくと、効率的にデバッグができる。

- 二分探索とは？
    - バイナリサーチ（Binary Search）とも呼ばれる
    - 指定の値がソート済みの配列のどこにあるかを、効率的に探索するアルゴリズムの一つ
    - 何かを探す際に探索範囲を半分に区切りながら探していく考え方
    - 怪しいと感じるコード範囲の真ん中あたりに仕込むことで、その範囲を分割することができる
        - もちろん、明らかに怪しいと感じる箇所があれば、初めからそこにプリントデバッグを仕込んでも構わない
    - 思い当たる原因が複数ある場合に二分探索の考え方が使える
    - 後はエラーが示す箇所に問題がないとき
- もっと大きな単位で二分探索する
    - フロント・サーバーサイド・インフラなどの大きな単位
    - フロントエンドとバックエンド、サーバーとデータベースなど物理的な境界が明らかな単位で分割していくのがオススメ
        - どんどん絞り込んでいく
        - 問題の切り分け
- Gitの履歴でも二分探索を使える
    - `git bisectコマンド`を使うことでどのバージョンで問題が発生したかを切り分けていくことができる

### 最小限のコードでデバッグする

効率的にデバッグするためには、まず不具合の原因と関係のなさそうな場所を排除して、見るべき範囲を狭めていくことが重要。

## デバッグ時の考え方

- 事前に「仮説」を立て、それを検証する
    - 「よく分からないけどとりあえずいじってみよう」はx
- 仮説を立てるためのテクニック
    - 思いつくままに原因となりそうなことを箇条書きにする
    - 箇条書きの中身をなるべく具体的かつシンプルにする
    - その過程で重複するものは排除、複数の要因があれば分割する
    - 最後に重要そうな順序に並び替える
- 一度に一つのことだけを検証する
    - 最初に立てた仮説が正しいのかだけに集中する

## デバッガ

- デバッガを使うと、処理を途中で止めることができる
    - その時点での変数の値を確認したりなどができる
- JSだとブラウザでデバッガを利用することができる
- ブレークポイント
    - 指定した場所でコードの実行を止めることができる
- 色々なステップ実行
    - ステップイン
        - 現在の行を実行し、1行進める
        - 全てのコードを1行ずつ丁寧に確認したい場合に使う
    - ステップオーバー
        - 現在の行のコードを実行し、次の行に進む 
        - 関数呼び出しがあった場合、関数の中には入らずに、関数呼び出しを実行して次の行に進む
        - ステップオーバーは、コードの全体像を把握しながら、ステップバイステップで実行を進めるのに役出つ
        - 1行ずつ実行するが、関数には入らないので、全体像を把握したい場合に使える
    - ステップアウト
        - 現在の関数の実行を完了し、戻り値を返した後に、呼び出し元に戻る
        - 関数内でデバッグを行なっているときに、関数から出て呼び出し元に戻るのに役立つ
        - ステップインで、デバッグの必要がない関数に入ってしまった場合に、関数の外に抜け出すために使う
- 「条件付きブレークポイント」を使うことで、特定の条件のときに処理をストップさせることができる
- VSCodeでもデバッガは使うことができる

## 情報収拾のための検索テクニック

- ダブルクオテーションで囲むことで、「完全一致」の検索をすることができる
- GitHub
    - 以下のように正規表現を使うことで`完全一致`の検索をすることができる
        - `/export function hoge/`
    - 以下のようにファイル名のパスで検索もできる
        - `path:hogefuga.js`

## エラーが見つからない場合

- 登場人物を確認する

## 不具合が再現できないときは？

- ユーザーから問い合わせなどが来たとき、まずは不具合が再現するかどうかを確認する
- 簡単に再現するなら、次のデバッグ作業に進むことができる
- 不具合を再現できないときは、まず不具合に関連する情報を集め、問題を切り分けることが重要
- これによって、再現に必要な「条件」を集めることができる
