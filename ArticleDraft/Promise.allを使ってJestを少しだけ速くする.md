この記事では、Promise.allを使ってJestの実行を少しだけ早くするTipsを紹介します。

## 事前のデータ生成を伴うテストについて

DBとの通信を要するアプリケーションの場合、以下のように事前にデータを生成した上でテストを実行する場合も多いと思います。

```js
test('サンプルテスト', async () => {
  await users.create([
    {
      id: 1,
    },
  ]);
  await posts.create([{ id: 10, userId: 1 }]);
  await comments.create([
    {
      id: 20,
      postId: 10,
    },
  ]);

...
```

このとき、非同期関数をawaitで並べてしまうと、それぞれのデータ生成処理が直列で実行されてしまうため、事前のデータ生成の部分で時間を消費してしまいます。

例えば、それぞれのデータ生成に3秒かかる場合、合計で9秒かかってしまうのです。

そこで利用するのが`Promise.all`です。

## Promise.allとは何か？

//

## Promise.allを利用してデータ生成処理を並列化する

参考: https://www.engilaboo.com/promise-async-await/