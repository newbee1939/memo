# ⭐️共有していない記事⭐️

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

# ⭐️共有した記事⭐️

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
