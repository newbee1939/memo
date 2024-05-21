## 概要

- Bunは`Node.jsの代替`となるJavaScriptランタイム
    - JavaScriptランタイムとは`JavaScriptを実行する環境`のこと
- 起動速度とメモリ使用量を劇的に下げる
- ランタイムだけでなく、テストやパッケージマネージャの機能も持っている
    - `ランタイムだけではないこと`がポイント
    - JavaScript/TypeScriptでアプリケーションを構築するための、まとまりのあるインフラ的なツールキットとなることが目標
- 既存のNode.jsプロジェクトでほぼ変更なしで使用することができる

## Bunの目的

- スピード
    - BunのプロセスはNode.jsより4倍速く起動する
    - `bun runはnpm runより約28倍速い`
    - `npm installからbun installに切り替えると、インストールが最大25倍高速化`
- TypeScriptとJSXのサポート
    - `.jsx、.ts、.tsxファイルを直接実行`することができる
    - Bunのトランスパイラでは、実行前にこれらをバニラJavaScriptに変換する
    - `ネイティブTypeScriptサポート`
        - Node.jsでTypeScriptを使うとき。tscでコンパイルしてから実行したり、ts-nodeやtsxを使う必要がある
        - 面倒
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
    - `BunはTypeScriptを直接実行できる`ため、本番環境で実行するためにTypeScriptをトランスパイルする必要はないかもしれない
    - Bunは実行するすべてのファイル（.jsと.tsの両方）を内部的にトランスパイルするため、.ts/.tsxソースファイルを直接実行することによる追加のオーバーヘッドはごくわずか
        - 追加の設定やトランスパイルなしに、TypeScriptファイルを直接コンパイルして実行できる
    - とはいえ、Bunを開発ツールとして使用していても、本番環境でNode.jsやブラウザをターゲットにしている場合は、トランスパイルする必要がある

## npmパッケージについて

- BunはNode.js APIとの完全な互換性を目指している
- Node.js環境向けのほとんどのnpmパッケージは、そのままBunで動作する

## コンパイル

参考: https://bun.sh/docs/bundler/executables

- Bunのbundlerは、TypeScriptやJavaScriptファイルからスタンドアロンのバイナリを生成するための`-compileフラグ`を実装している
    - `bun build ./cli.ts --compile --outfile mycli`
    - `./mycli`で実行できる

## 本番環境へのデプロイ

- `コンパイルされた実行ファイルはメモリ使用量を削減し、Bunの起動時間を改善する`
- 通常、Bunはimportやrequire時にJavaScriptやTypeScriptファイルを読み込んでトランスパイルする
- これはBunの多くを「ただ動く」ものにしている部分ですが、無料ではない
- ディスクからのファイルの読み込み、ファイルパスの解決、解析、トランスパイル、ソースコードの印刷に時間とメモリがかかる
- `コンパイル済みの実行ファイルを使えば、そのコストをランタイムからビルドタイムに移すことができる`
- 本番環境にデプロイする際のオススメの設定は以下の通り
    - `bun build --compile --minify --sourcemap ./path/to/my/app.ts --outfile myapp`

## 環境変数

- Bunは以下のenvファイルを自動的に読み込む
    - .env
    - .env.production, .env.development, .env.test (depending on value of NODE_ENV)
    - .env.local
- `dotenv`は不要

## Auto-install

TODO: この辺りもう少し深く理解する

- 作業ディレクトリ以上に`node_modulesディレクトリが見つからない場合`、BunはNode.jsスタイルのモジュール解決を放棄し、`Bunモジュール解決アルゴリズムを使用する`
- Bunスタイルのモジュール解決では、インポートされたすべてのパッケージは、実行中にグローバルモジュールキャッシュにオンザフライで自動インストールされる（bun installで使用されるのと同じキャッシュ）
- 以下のスクリプトを最初に実行すると、Bunは "foo "を自動インストールしてキャッシュする
- 次にスクリプトを実行するときは、キャッシュされたバージョンが使用される

```ts
import { foo } from "foo"; // `最新版` をインストールする。

foo()；
```

インストールするバージョンを決定するために、Bunは以下のアルゴリズムに従う。

1. プロジェクトルートに`bun.lockb`ファイルがあるかチェックする。存在する場合は、lockfileで指定されたバージョンを使用する
2. そうでない場合は、依存関係として "foo "を含むpackage.jsonをツリー上でスキャンする。見つかった場合、指定されたsemverバージョンまたはバージョン範囲を使用する
3. そうでない場合は、最新のものを使用する

バージョンまたはバージョン範囲が決定されると、Bunは次のことを行う。

1. 互換性のあるバージョンがないかモジュールキャッシュをチェックする。存在する場合はそれを使う
2. latestを解決するとき、Bunはpackage@latestが過去24時間以内にダウンロードされ、キャッシュされているかどうかをチェックする。存在する場合はそれを使う
3. そうでない場合は、npmレジストリから適切なバージョンをダウンロードしてインストールする

### Auto-installのメリットについて

- スペース効率 
    - 依存関係の各バージョンは、ディスク上の1つの場所にのみ存在する
    - これは、冗長なプロジェクトごとのインストールに比べて、スペースと時間の大幅な節約になる
- Portability
    - シンプルなスクリプトやgistを共有するために、ソースファイルは自己完結している
    - コードや設定ファイルを含むディレクトリをzipでまとめる必要はない
    - `import文でバージョンを指定すれば、package.jsonも不要`
- 利便性 
    - ファイルやスクリプトを実行する前に `npm install や bun install を実行する必要はない`
    - bunで実行するだけ

## bunfig.toml

- Bunの動作は、設定ファイルbunfig.tomlを使って設定することができる
- 一般的にBunは、package.jsonやtsconfig.jsonのような既存の設定ファイルに依存して動作を設定する
- bunfig.tomlは、Bun固有のことを設定する場合にのみ必要
- このファイルはオプションであり、Bunはこのファイルがなくてもすぐに動作する

参考: https://bun.sh/docs/runtime/bunfig

## Debugger

https://bun.sh/docs/runtime/debugger

## Lockfile

- `bun install`を実行すると、`bun.lockb`が生成される
- bun.lockbはバイナリ形式
    - パフォーマンスのため
    - Bunのロックファイルは保存と読み込みが驚くほど速く、一般的なロックファイルよりも多くのデータを保存している

## 参考資料

- [Bun: 公式ドキュメント](https://bun.sh/docs)
- [Bun's Roadmap](https://github.com/oven-sh/bun/issues/159)
- [You don't need Node.js](https://zenn.dev/nakasyou/articles/you_dont_need_node)
- [100秒で理解するBun](https://zenn.dev/ak/articles/c21609fd3b0fdc)

## TODO

- TODOの部分をやる
- より深く調べる