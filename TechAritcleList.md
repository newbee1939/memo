## Rust製ブラウザエンジン「Servo」搭載、新たなWebブラウザ「Verso」の開発プロジェクトが立ち上がる

Versoの開発は、Electron代替を目指すフレームワーク「Tauri」の開発チームが主導する。

https://www.publickey1.jp/blog/24/rustservowebverso.html

## Google Cloud Next Tokyo '24 Day1 & Day 2 基調講演でのアップデートを纏めました #GoogleCloudNext

https://dev.classmethod.jp/articles/google-cloud-next-tokyo-24-keynote-update/

## JavaScriptの多用はSEOに悪影響なのか？Vercelが徹底的に調査、結果は？

結論、悪影響はない。
ただ、Google以外はどうなのか？

https://techfeed.io/entries/66aab0774d86d6263dcf93f3

## ライアン・ダール、DenoにおけるHTTPインポートの設計の誤りを率直に認める — JSRへの移行を推奨

https://techfeed.io/entries/66a962d6f1f6865688fd343d

## GraphQL 界の Babel こと Envelop を使ってスキーマの破壊的変更をごまかす

https://zenn.dev/layerx/articles/c34b307527988f

## sqlc を TypeScript で利用する

生クエリでパフォーマンスを追求しつつ、TSの型の恩恵も得られる。
良さそうだがあまり流行ってない？

https://zenn.dev/shiguredo/articles/sqlc-gen-typescript

## エキサイトのDB設計（DBのテーブル構造のアンチパターンと改善）

テーブルに状態を持たせない。細かくテーブルを分割する。
やや過激な思想だけど参考になる部分はありそう。

https://tech.excite.co.jp/entry/2021/04/05/164232

## Dockerfileを解析、最適化やベストプラクティスをガイドしてくれる「Docker Buildチェック」機能が正式版に

https://www.publickey1.jp/blog/24/dockerfiledocker_build.html

- Docker Buildチェックの機能では、Dockerfileの構文をチェックし、ビルドが最後まで正常に実行できるかどうかを確認する機能だけでなく、最適化されたDockerfileによるビルド時間の短縮や、コミュニティから収集し体系化した一連のベストプラクティスを学べるようにガイドする機能なども提供される
- Dockerfileなどを変更した場合に実際に全体をビルドすることなく、通常は1秒未満で高速にビルドの評価だけを行うこともできる

詳細: https://www.docker.com/ja-jp/blog/introducing-docker-build-checks/

## 静的サイトジェネレータのAstro、「Server Islands」を実験的実装。サーバで動的生成したコンポーネントをWebページ表示後に組み込み

リンク: https://www.publickey1.jp/blog/24/astroserver_islandsweb.html
Server Islandsのデモサイト: https://server-islands.com/

- 今回、Astro 4.12で実験的実装が行われた「Server Islands」は、ユーザーごとにパーソナライズされる情報など、サーバ側で動的に生成されるコンポーネントを、「Islands」と同様にWebページ上にあとから組み込むことで、高速なWebページの表示を維持したまま、より動的なWebサイトの構築を実現するための仕組み  
- Server Islandsでは、Webブラウザからのリクエストに対して、まずすべてのユーザーに静的生成されたHTMLが返され、高速にWebページが表示される
- パーソナライズが必要なコンポーネントの部分にはプレイスホルダーが埋め込まれている

## デバッグのときにDockerコンテナにシェルやデバッグツール群を組み込める「Docker Debug」が正式リリース

https://www.publickey1.jp/blog/24/dockerdocker_debug.html

- Docker社は、デバッグしたいときにDockerコンテナにシェルやデバッグツール群を組み込める`Docker Debug`の正式リリースを発表
- 「Docker Desktop 4.33」に含まれている
- 一般にDockerコンテナは、使用メモリの最小化とセキュリティを高めるなどの目的で、シェルやツールなどを徹底的にそぎ落としてスリム化したOSの上にアプリケーションを載せた構成にする
- そのため、コンテナ内のアプリケーションに問題が発生した場合に、エディタやデバッガなどを使って状況を確認し、デバッグをしようとしても、pingやviといったコマンドはおろかコマンドラインを提供するシェルも用意されていない環境に対してデバッグを始めなければならない、といった状況が発生する
- これを解決するのが「Docker Debug」
- Docker Debugは、任意のコンテナやイメージに対してシェルとvim、nano、htop、curlなどのデバッグに利用できるツール群を、必要になったときに簡単に組み込むことができる

## WebホスティングのNetlifyがAstroと提携、静的サイトジェネレータAstroのオフィシャルなデプロイメントパートナーに

https://www.publickey1.jp/blog/24/webnetlifyastroastro.html

- Webホスティングサービスを提供するNetlifyは静的サイトジェネレータ「Astro」開発チームの両者は提携を発表し、NetlifyがAstroのオフィシャルデプロイパートナーとなったことを発表した
- Netlifyは今回、Astroと提携することによって、Webホスティングサービスとしてオフィシャルに提供できるWebサイトのフレームワークの幅を増やしたことになる

# ⭐️共有していない記事⭐️

# ⭐️共有した記事⭐️

## Node、Deno、Bun?Node代表古川さんと学び直す JS Runtimeの歴史とこれから

https://offers-jp.connpass.com/event/327428/

## VisualStudioCodeで絶対にしておくべき設定ベスト20

https://zenn.dev/llm_robot/articles/20240731-vscode-settings-extensions-theme

`files.autoSave`で自動保存できるのは知らなかった。

タスクの設定も。

## f.luxで眼精疲労を軽減

- f.lux はハーバード大学医学部が推奨するディスプレイの色温度を場所と時間に合わせて調節するクロスプラットフォームのブルーライトカットソフトウェア
- このプログラムは夜間の眼精疲労と睡眠パターンの乱れなどの生活習慣病を軽減することを目的に作成された
- f.luxをインストールする際に利用者は地理座標、郵便番号、あるいは地名に基づいて場所を選択する
- すると、選択された場所の日の出と日の入りの時刻に基づいてディスプレイの色温度が自動的に調整される
- 日没時には色温度が徐々に暖色に変化し、日の出時には元の色(寒色)に戻る
- 夜のブルーライトはメラトニンの分泌を減少させ、がんや心臓病、糖尿病、肥満などの生活習慣病の発症リスクを高める要因の一つとされている
- このため、夜間、ハーバード大学医学部では、f.luxなどのブルーライトカットソフトを強く勧めている

https://ja.wikipedia.org/wiki/F.lux
https://justgetflux.com/

- MacのNight Shiftとの違いについて
  - https://www.lifehacker.jp/article/170414_night_shift_flux/
  - どちらを使うかは、あなたがどのぐらい設定をいじりたいかにもっぱら左右される
  - 設定オプションの豊富さでは圧倒的にf.lux
  - 効果が控えめなのはNight Shift

## 世界中の大学のコンピュータサイエンスやプログラミング講座が日本語で学べる「MOOC」（大規模公開オンライン講座）サイトまとめ。2024年版

https://www.publickey1.jp/blog/24/moocmassive_open_online_courses2024.html

## GitHub、AIアプリ開発環境「GitHub Models」発表。主要なAIモデルをプレイグラウンドで評価、アプリへの組み込みまでシームレスな環境を提供

https://www.publickey1.jp/blog/24/githubaigithub_modelsai.html 

## 徳丸浩氏に聞く、クレカ情報の非保持化に潜む漏洩リスクとEC事業者の対策

- クレジットカード情報は、2018年に施行された改正割賦販売法にもとづき、ECサイトやWebサービスの運営事業者では事実上、保持しないこと（非保持化）が義務付けられているなか、なぜ漏洩被害が発生してしまうのか？
- ECサイトでクレジットカード情報の漏洩事案が発生するのは、ECサイトの利用者がクレジットカード情報を入力する決済画面から情報が窃取（Webスキミング）されるため
  - ECサイト事業者のデータベースにクレジットカード情報が保存されておりそれが盗まれるというわけではない
- 攻撃には、JavaScript型の決済代行を狙うものと、画面遷移型の決済代行を狙うものがあり、前者には10年以上同じ手口が使われている
- クレジットカード情報の非保持化をしていても、セキュリティ対策は必須
- 有効な対策としては、脆弱性対応やパスワード管理、WAF導入などのWebセキュリティの基本が最優先
- 次いで重要なのが改ざん検知であり、導入により漏洩のリスクや被害を大幅に低減できる
- クレカ情報の漏洩が発生した場合、ECサイトを一時停止することが最優先
- その後、決済代行業者やフォレンジック調査業者と連携しながら対応する
- 事案の対外的な公表は、クレジットカード会社とECサイト事業者が協議のうえ、同時に行うことが一般的

---

- クレジットカードの不正利用は大きく分けて、偽造クレジットカードによるものと番号盗用によるものがある
- 日本クレジット協会のデータでは、前者の被害額が減少しているのに対し、後者の被害額は2014年以降、年々増加している  
  - 番号盗用の原因としては、フィッシングによるものや原因不明と分類されるものもありますが、日本クレジット協会が開催した過去のセミナーでは「ECサイトからの漏洩が大半」だと説明されている
- 少なくとも、事実として言えることとしては、直近でもECサイトはクレジットカード情報を漏洩するようなセキュリティ被害を受け続けており、また漏洩事案あたりのクレジットカード情報の漏洩件数も多い状況が続いている

https://unitis.jp/articles/12277/

## 2024年版のDockerfileの考え方＆書き方

https://future-architect.github.io/articles/20240726a/

## How to choose the best rendering strategy for your app

https://vercel.com/blog/how-to-choose-the-best-rendering-strategy-for-your-app

## 「生成AI検索」は著作権侵害なのか？　日本新聞協会の“怒りの声明”にみる問題の本質

https://www.itmedia.co.jp/news/articles/2407/26/news175.html

## Node.jsのTypeScriptサポートについて

https://gist.github.com/azu/ac5dafbf211ef8b5ecf386930ac75250

## diffを見やすくする difftastic を導入する

文法レベルでdiffを表示してくれる。

https://zenn.dev/mobdev/articles/c1ecb5a3ce9e89

## 【怖い】経緯を読んだらガチの国際クライムサスペンスだった→フリーのエンジニアを狙ったサイバー攻撃が増加中

海外のリモートワーク求人サイトでの案件でサイバー攻撃に遭いかけた人の話。
意図せず攻撃を実行している可能性もあるので注意..

https://togetter.com/li/2405557

## IT エンジニア的にとても困る名前のアイドルグループがデビュー→「狙ってますねこれは」「検索汚染が起きる」「姉妹グループはUTF8」

UNICODEというグループでデビュー曲の名前はHELLO WORLD。

https://togetter.com/li/2406620

## 【海外で話題】Linuxシステムコールの一覧表が突如登場して話題に、カーネルソースコードへのリンクも網羅

https://techfeed.io/entries/669ecf9e49428337f0cf1680

https://syscalls.mebeim.net/?table=x86/64/x64/latest

## Next.js って App Router が出てきて平和じゃなくなったよね

- 新規で作るならApp Routerでもいい感じに作れる？
- 移行するのはなかなか厳しそうかも

https://zenn.dev/noko_noko/articles/3ccc64c389259c

## Google Docs、Markdown形式でのドキュメントのエクスポート、インポートなど可能に

VSCodeでMarkdownで書いたドキュメントなどをインポートできるように。

https://www.publickey1.jp/blog/24/google_docsmarkdow.html

## Cloudflare D1

プライマリサーバーは1台でそこに書き込む。
書き込まれたら各エッジサーバーに分散配置される（シャーディング）

https://www.cloudflare.com/ja-jp/developer-platform/d1/

Prismaも対応してきている。

https://www.prisma.io/docs/orm/overview/databases/cloudflare-d1

## Nile database

[Neon](https://neon.tech/)の対抗馬的な立ち位置？

https://www.thenile.dev/

## Google、サードパーティークッキー廃止方針を撤回

https://www.nikkei.com/article/DGXZQOGN2305Y0T20C24A7000000/

## Refined GitHub

GitHubの機能を拡張してくれるChrome拡張。
tabが効くのはありがたい。

https://chromewebstore.google.com/detail/refined-github/hlepfoohegkhhmjieoechaddaejaokhf

https://github.com/refined-github/refined-github/blob/main/readme.md

## Google、アプリ実行時に生成AIが適切なUIを構成し動的生成する「AI Generated UI」発表

- アプリケーションの実行時に生成AIが適切に構成して動的に生成し表示する
- 現時点でAI Generated UIはFlutterフレームワークの上にアーリープレビューとして実装されている
- ユーザーの意図に基づいてFlutterが動的にUIコンポーネントとレイアウトを構成
- ユーザーにパーソナライズされた最適なUIを表示する
- GoogleはこのAI Generated UIを、Flutterが対応するモバイルからWebまでのあらゆるアプリケーションに搭載するとしている

https://www.publickey1.jp/blog/24/googleaiuiai_generated_ui.html

## 開発者のためのスライド作成ツール Slidev がすごい

- マークダウン形式でのスライド作成ツール
- 機能
  - 柔軟なマークダウン記法によるスライド作成
  - 視認性の高いコードスニペット & ライブコーディング
  - 多彩な表示モード
  - プレゼンテーションの録画機能

https://zenn.dev/ryo_kawamata/articles/introduce-slidev

## アーキテクトの教科書 価値を生むソフトウェアのアーキテクチャ構築

買ってみた。
ぱっと見初心者向けな印象。

https://amzn.asia/d/08p1eGv0

## なぜ令和のエンジニアに呆活（ぼうかつ）が必要なのか

- 呆活とは文字通りぼーっとすること
-  ぼーっとしてる状態は脳科学的な観点で言うと、デフォルト・モード・ネットワークという神経回路が活性化しており、リラックス効果や記憶の整理整頓、ひらめきなどを生み出す効果があると言われている
- おススメの呆活３選
  - 散歩
  - カフェ
  - 温泉

https://tech.nri-net.com/entry/why_engineers_need_to_be_zoned_out

## Next.js って App Router が出てきて平和じゃなくなったよね

- App Router導入で考えないといけないこと
  - ディレクトリ設計の検討
    - App Router の環境下では、layout.tsxとtemplate.tsxという特別なファイルを作成でき、そのファイルを設計に組み込むかどうかで、ディレクトリ設計に影響が出てくる
  - コンポーネント設計の検討
  - Server Actions の検討
  - データキャッシュの検討

https://zenn.dev/noko_noko/articles/3ccc64c389259c

## CSSにif文が追加されるらしい

参考: https://zenn.dev/persona/articles/cfbc6a6b9552a6

e.g.

```css
.element {
  background-color:
    /* If the style declares the following custom property: */
    if(style(--variant: success),
      var(--color-green-50), /* Matched condition */
      var(--color-blue-50);  /* Default style */
    );
}
```

## JavaScriptを大きく変えうる Dataflow Proposals の概要と論点(Call-this, Pipe Operator)

処理の順番をより明確に記述できるようになる。

参考: https://zenn.dev/yuku/articles/b169ac62ac3271

```js
// Before
const publicArticles1 = (await fetch("/articles", {
  headers: { Authorization: await getIdTokenFromAuth.call(getAuth()) },
})).filter((a) => isPublic(a));

// After
const publicArticles2 = getAuth()
  ~> getIdTokenFromAuth()
  |> await fetch("/articles", { headers: Authorization: @ })
  .filter(isPublic~(?));
```

## 開発部に不満を持っていたCSがエンジニアにジョブチェンしてわかった「勝手に諦めない」ことの大切さ

コミュニケーションで勝手に諦めない。

参考: https://speakerdeck.com/sakuraikotone/kai-fa-bu-nibu-man-wochi-tuteitacsgaenzinianiziyobutiensitewakatuta-sheng-shou-nidi-menai-kotonoda-qie-sa

## 君たちはどうコードをレビューする (される) か

参考: https://speakerdeck.com/utgwkk/da-ji-xiang-si-dot-pm

## SuspenseとAlgebraic Effects

```
Algebraic Effectsは研究用プログラミング言語などで実装されている仕組みで、使われているのはOCamlやLISPなどの関数型言語くらい。他にはalgebraic effectsを言語機能として初めて設計したEffという言語がある。まだまだ一般的になるには時間がかかりそう...というものらしい。
Reactを使う上で気にする必要はあまりない概念ではあるけど、Reactコアチームで、HooksやSuspenseを考案したSebastianは「これが私たちが React の中でやってることのメンタルモデルなんですよ」と言っているとのこと。
```

参考: https://scrapbox.io/teamlab-frontend/Suspense%E3%81%A8Algebraic_Effects

## Temporal

```
Date は ECMAScript において長年の悩みの種でした。Temporal はモダンな date/time API を ECMAScript にもたらします
```

Dateの代わりに使われるようになる？

参考: https://tc39.es/proposal-temporal/docs/ja/

## ESLintがJavaScript以外にも対応言語を広げるとの方針を説明。まずはJSON、Markdownへの対応プラグインを開発

- 公式のプラグインとしてJavaScript、JSON、Markdown対応の3つが登場する
- 多言語対応により開発がシンプルになる
- パッケージ管理のコストは増える？

参考: https://www.publickey1.jp/blog/24/eslintjavascriptjsonmarkdown.html

## Google本社の方に聞いたいい開発者になるための習慣

- より良い開発者になるためのマインド
  - 自分より技術がある人にコードを見せて積極的にコードレビューをもらう
  - 早く失敗してどんどん繰り返す
  - ドキュメント
    - 優秀なエンジニアはそのコードがどういう仕組みで動いているのかなどを理解し文書化できる
  - 知識を共有する
    - 自分の勉強した知識などをどんどん周りに話す。アウトプット精神
  - 他人を非難しない
    - Googleでは何か問題があっても問題を起こした本人を責めたりしない
    - 問題が起こった時はその問題の解決に集中する
- AI時代でも生き残るのに必要な能力
  - AIでも理解できないような複雑な要求事項を理解する力
  - 技術コミュニケーション力

参考: https://qiita.com/bisketoriba/items/116e73224232703b3965

## なぜ宣言的 UI は壊れにくいのか / Why declarative UI is less fragile

- 手続きは前の状態に依存する
  - 手続きは「モード」を発生させる
- 宣言的UIはモードレスなので、変更時に壊れにくい

- 大きな流れとしては、`宣言的プログラミング`に傾いている
  - Zodとかもそんな感じ

参考: https://speakerdeck.com/uenitty/why-declarative-ui-is-less-fragile

## 集中して作業する技術

- 運動・睡眠
- スマホを遠くに置く
- 机に余計なものは置かない
- 1度に1つのことをやる
- コミュニケーションの遮断
- 視覚・聴覚を制限
  - 個人差ありそう
- プチ瞑想

参考: https://speakerdeck.com/hanhan1978/how-to-work-deeply

## Web Developer Conference 2024

参考: https://web-study.connpass.com/event/321711/

## AI時代は「質問力」が最大の武器になる→マジの研究者の人が本気で、だけど完全な初心者にもわかるようにプロンプトを解説した本「AI時代の質問力」に興味津々

参考: https://togetter.com/li/2402018

## ロードバランサーってなんやねん

- 負荷分散には以下二つの主要なアルゴリズム(手法)がある
  - 静的負荷分散アルゴリズム：事前に決められたルールに基づいてリクエストを分配する
  - 動的負荷分散アルゴリズム：リアルタイムにサーバーの状態や負荷に基づいてリクエストを分配する
- サーバーの死活監視も行う
  - ロードバランサーは接続されているサーバーの稼働状態を監視し、問題が発生したサーバーを即座に検出してトラフィックの流れを調整する

参考: https://zenn.dev/mi_01_24fu/articles/load-balancer_2024_07_13

## スマホゲーム業界におけるPHPの歴史とLaravel Octaneで広がるこれからのPHP

Laravel Octaneは、アプリケーションの起動後全ての処理をメモリ上にロードした状態を維持しリクエスト間で使い回すことによって、高速なアプリケーションを提供するツール。

https://developers.cyberagent.co.jp/blog/archives/35832/

## Laravel Herd

Herdは、macOS向けの高速で便利なネイティブなLaravelとPHPの開発環境。

参考: https://herd.laravel.com/

## Vitest: In-Source Testing

VitestはViteのtestingツール。
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
    - RAGなどのAI開発の需要も関係している？
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
  - 暗号化しているといっても、秘匿情報をリポジトリで管理するのは？

参考: https://zenn.dev/moozaru/articles/edb09434f0680b

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
