# ⭐️共有していない記事⭐️

## スマホゲーム業界におけるPHPの歴史とLaravel Octaneで広がるこれからのPHP

Laravel Octaneは、アプリケーションの起動後全ての処理をメモリ上にロードした状態を維持しリクエスト間で使い回すことによって、高速なアプリケーションを提供するツール。

https://developers.cyberagent.co.jp/blog/archives/35832/

## Laravel Herd

Herdは、macOS向けの高速で便利なネイティブなLaravelとPHPの開発環境。

参考: https://herd.laravel.com/

## Vitest: In-Source Testing

実装とテストを同一ファイルに書ける。

https://vitest.dev/guide/in-source

## Macなどの高精細なディスプレイでVSCodeの文字を見やすくする簡単な方法

https://zenn.dev/naas/scraps/78547d41464e5d

## ChatGPTはコーディングが不得意？2021年以降の問題が顕著に苦手 ー AI生成コードに関する調査結果

参考: https://techfeed.io/entries/668c54af46112d2a8da23a3b

## サイバーエージェント、新たな日本語特化LLMを一般公開　「Llama-3-70B」と同等の日本語能力　商用利用も可

参考: https://www.itmedia.co.jp/aiplus/articles/2407/09/news118.html

## Node.jsでTypeScriptのコードを実行できるようになるかも

参考: https://hiroppy.me/blog/nodejs-strip-type/

- Node.jsと同じ立ち位置であるDenoやBunはTypeScriptをネイティブサポートしているが、Node.jsはサポートしていない
- なので普段、TypeScriptを利用するときにはts-nodeやtsxなどが必要
- `--experimental-strip-types`というフラグを実行時に付けることにより、Node.jsでTypeScriptのコードを実行できるようになるかも

## MySQL 9.0登場。 JavaScriptストアドプログラムが利用可能に、ベクトル型もサポート

参考: https://www.publickey1.jp/blog/24/mysql_90_javascript.html

- JavaScriptストアドプログラム
  - ストアドプログラムをJavaScriptで記述できるように
  - ベクトル（Vector）型をサポート
  - Explain Analyzeの結果をJSON形式で出力可能に

## [Astro×Hono×Fresh対談] Next.jsじゃないFWが見据えるフロントエンドの未来

2024/07/25(木)
19:00 〜 20:30

参考: https://offers-jp.connpass.com/event/324687/

## 暗号化に対応した次世代dotenvツールdotenvxを使う

- 広く使われている環境変数をファイルで管理するdotenvの次世代版 dotenvxのv1.0がリリース された
- 作者はdotenvを作ったMotさん
- 正式な次世代版
- dotenvxはdotenvの弱点を克服したものになっている
- dotenvファイル自体が暗号化され、Gitでバージョン管理でき、そのままデプロイして環境変数を適用できるかも？

参考: https://zenn.dev/moozaru/articles/edb09434f0680b

# ⭐️共有した記事⭐️

## VSCoee拡張: Turbo Console Log

コマンド一つでconsole.logを追加・削除できるVSCode拡張。

https://marketplace.visualstudio.com/items?itemName=ChakrounAnas.turbo-console-log

```json
{
  "turboConsoleLog.addSemicolonInTheEnd": true,
  "turboConsoleLog.insertEnclosingClass": false,
  "turboConsoleLog.insertEnclosingFunction": false,
  "turboConsoleLog.quote": "'",
  "turboConsoleLog.wrapLogMessage": true
}
```

上記の設定の場合、以下のように出力される。

```ts
console.log('🚀 --------------------------------------------------------🚀');
console.log('🚀 ~ allaboutRankingQueryData:', allaboutRankingQueryData);
console.log('🚀 --------------------------------------------------------🚀');
```

## Cloud Run のボリューム マウントのご紹介: アプリを Cloud Storage や NFS に接続

参考: https://cloud.google.com/blog/ja/products/serverless/introducing-cloud-run-volume-mounts

- コンテナからストレージに、ローカルファイルであるかのようにシームレスにアクセスできるようになる
- 使える場面
  - 秘密にしておく必要のない構成データの保存
  - 静的なウェブサイトの提供
    - 使える場面はありそう

## 増田さんに聞く！ ドメイン駆動設計の実践技法

2024/07/25(木)
12:00 〜 13:00

https://findy.connpass.com/event/323023/?utm_campaign=event_participate_to_follower&utm_source=notifications&utm_medium=twitter

## フルリモートで相手に気持ちよく仕事をしてもらうためのコツあれこれ

参考: https://zenn.dev/praha/articles/897f354bb76b98

- 何かを教えてもらう→「知ってました」と言わない
- 「前も言った気がしますが」とか言わない
- 「はい/いいえ」で答えられる質問には、先に「はい/いいえ」で答える
- 質問するときは「はい/いいえ」で答えられる文章にする

## JSライブラリ「Polyfill.io」がマルウェアに改変、10万サイト以上に影響

買収後にマルウェアに改変されたらしい。

https://news.mynavi.jp/techplus/article/20240628-2974852/

## NTTデータ、国産LLM「tsuzumi」を「Microsoft Azure」で提供

NTT研究所が40年以上にわたって蓄積した自然言語処理技術をベースに開発され、高性能ながらパラメーターサイズが6億～70億と海外のLLMより軽量な点が特徴。

https://japan.zdnet.com/article/35220726/

## OpenSSHの脆弱性について

放置しておくと SSH を受け付ける全てのサーバーを乗っ取る事ができてしまう脆弱性。

https://zenn.dev/cloud_ace/articles/cve_2024-040

## デッドライン迎えたKADOKAWA｢サイバー攻撃｣。流出した内部文書、ユーザーが今できる3つのこと

ニコニコ登録している人&パスワード使いまわしている人は変更必須。

https://www.businessinsider.jp/post-289589

## Vite（ヴィート）ってよく聞くけど何なんですか？ あれは

参考: https://zenn.dev/comm_vue_nuxt/articles/what-is-vite

- 次世代フロントエンドツール
- フロントエンドの開発を行う上で必要な周辺環境を良い感じにまとめてくれているもの
- 具体的には以下のようなもの
  - TypeScript, JSX, CSS, ...
  - 開発サーバー
  - HMR
  - バンドラ
  - プラグインシステム
- Vite は何より、より良い DX (開発者体験) にフォーカスしている
- 伸びてそう
  - https://npm-compare.com/vite/#timeRange=FIVE_YEARS

## Vitestに入門しよう

参考: https://zenn.dev/ryohei0509/articles/c9dc69296a0445

- HMRによるテストの高速化
  - HMRは、ソースコードの変更を検出し、関連するテストだけを即座に実行できるため、変更による影響をすぐに把握できる
- 高速なビルドツールであるViteをベースにしている
