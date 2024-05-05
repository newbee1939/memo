## エラーと例外

参考: https://zenn.dev/kojikaya/articles/ad6903f3f6bbc8

- Javaのエラー、例外に関するクラスは全て `Throwableクラス`配下にある
- Throwableクラスのサブクラスとして`Errorクラス`、`Exceptionクラス`がある
- Exceptionクラスにはサブクラスとして`RuntimeExceptionクラス`と`その他のクラスである検査例外`に分類される

### Errorクラス

- `Errorクラス`は`プログラムではどうしようもない事態`が起きた際に発生する
- 例えば以下のような
    - StackOverflowError(スタック領域のオーバーフロー)
    - OutOfMemoryError(メモリの不足)
- これらのエラーはプログラムではどうしようもないものなので、例外ハンドリングする意味がない
- try-catchを記載しても、catchすることができずにErrorとなる

### 検査例外と非検査例外

- 非検査例外とは
    -  RuntimeExceptionクラス配下の例外クラスが対象
    - 非検査例外は try-catchが必要ないため、「非」検査例外と言われる
    - `非検査例外`は`文法上のエラーはない`ので、コンパイルエラーにはならない
    - 実行時のエラーとして例外メッセージが表示される
        - ex. NullPointerException(ヌルポ)
        - ex. IllegalArgumentException(不正な引数をメソッドに渡した)
    - 非検査例外は正しいプログラムを書くことで回避することのできる例外
- 検査例外とは
    - 検査例外は try-catchが必要な例外のため検査例外と言われる
    - catch しなければ、コンパイルエラーが発生するため、例外ハンドリングが必須
        - ex. SQLException(DB系の例外)
        - ex. IOException(入出力関係の例外)
- 検査例外と非検査例外はJava特有の仕様
    - ほとんどのプログラミング言語では例外は基本的に全て`非検査例外`としている