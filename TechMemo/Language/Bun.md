## 概要

- Bunは`Node.jsの代替`となるJavaScriptランタイム
- 起動速度とメモリ使用量を劇的に下げる
- ランタイムだけでなく、テストやパッケージマネージャの機能も持っている
    - `ランタイムだけではないこと`がポイント
    - JavaScript/TypeScriptでアプリケーションを構築するための、まとまりのあるインフラ的なツールキットとなることが目標
- 既存のNode.jsプロジェクトでほぼ変更なしで使用することができる

## Bunの目的

- スピード
    - BunのプロセスはNode.jsより4倍速く起動する
    - `bun runはnpm runより約28倍速い`
- TypeScriptとJSXのサポート
    - .jsx、.ts、.tsxファイルを直接実行することができる
    - Bunのトランスパイラでは、実行前にこれらをバニラJavaScriptに変換する
- ESM & CommonJSの互換性
    - BunはしっかりとCommonJSもサポートしている
- Web標準のAPIも多数搭載されている
    - `fetch`、`WebSocket`など
- Node.jsとの互換性も担保している

## Bunのインストール

参考: https://bun.sh/docs/installation

- Mac
    - `curl -fsSL https://bun.sh/install | bash # for macOS, Linux, and WSL`

## QuickStart

- `bun init`でプロジェクトを開始できる
- BunでシンプルなHTTP serverを実装する
```javascript
const server = Bun.serve({
  port: 3000,
  fetch(req) {
    return new Response("Bun!");
  },
});

console.log(`Listening on http://localhost:${server.port} ...`);
```

## TypeScript

- BunのTypeScriptの型をインストール
    - `bun add -d @types/bun # dev dependency`
- `bun init`で`tsconfig.json`が生成される

## bun run コマンド

- ファイルの実行
    - 以下のどちらでも実行できる
        - `bun run index.ts`
        - `bun index.ts`
- watchモードで実行
    - `bun --watch run index.tsx`
- `bun run --smol`
    - メモリに制約のある環境では、-smolフラグを使用して、パフォーマンスを犠牲にしてメモリ使用量を削減することができる

## トランスパイラについて

- トランスパイラは必要か？
    - BunはTypeScriptを直接実行できるため、本番環境で実行するためにTypeScriptをトランスパイルする必要はないかもしれない
    - Bunは実行するすべてのファイル（.jsと.tsの両方）を内部的にトランスパイルするため、.ts/.tsxソースファイルを直接実行することによる追加のオーバーヘッドはごくわずか
    - とはいえ、Bunを開発ツールとして使用していても、本番環境でNode.jsやブラウザをターゲットにしている場合は、トランスパイルする必要がある

## npmパッケージについて

- BunはNode.js APIとの完全な互換性を目指している
- Node.js環境向けのほとんどのnpmパッケージは、そのままBunで動作する

## コンパイル

参考: https://bun.sh/docs/bundler/executables

- Bunのbundlerは、TypeScriptやJavaScriptファイルからスタンドアロンのバイナリを生成するための-compileフラグを実装している
    - `bun build ./cli.ts --compile --outfile mycli`

## 環境変数

- Bunは以下のenvファイルを自動的に読み込む
    - .env
    - .env.production, .env.development, .env.test (depending on value of NODE_ENV)
    - .env.local
- `dotenv`は不要

## その他

## 参考資料

- [Bun: 公式ドキュメント](https://bun.sh/docs)