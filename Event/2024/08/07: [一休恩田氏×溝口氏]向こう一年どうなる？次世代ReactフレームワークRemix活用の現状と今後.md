# [一休恩田氏×溝口氏]向こう一年どうなる？次世代ReactフレームワークRemix活用の現状と今後

リンク: https://offers-jp.connpass.com/event/324745/

## 内容メモ

### 【LT1】Remix の細かすぎて伝わらない好きなところ

スライド資料: https://www.docswell.com/s/8723156/ZQR837-2024-08-07-172936#p1

- Remixの魅力
  - 一番の魅力は`We標準`がベースになっている点
    - 仕様の安定性
  - 妙な抽象化やブラックボックスがない
    - コードを追えば、全てが分かる
  - クリアなデータフロー
    - loader / component / actionのサイクルで、コンパクトに責務を分離
    - useState, useEffect不要
  - 「段階的に強化」ができる
    - 最低限の機能性で一旦リリース
    - 後で時間ができたら色々工夫してUX向上
      - みたいな
  - SPA modeが超イイ
    - APIサーバーがある前提での業務用Webアプリに最適
    - SSRと同じように、責務を分けてクリアに書ける
    - 普通のSPAに比べ状態管理ほぼ不要に
  - つらいReact Server Component(RSC)対応が不要
  - （将来性の面）最もダウンロードされているReactフレームワークになりそう
    - 次のバージョンRemix v3はReact Router v7という名前になる
    - React RouterはNext.jsより多くダウンロードされている

### 【LT2】 Web標準の力: Remix Wayを外れる自由~フレームワークに縛られない開発を実現するRemix~

スライド資料: https://speakerdeck.com/takonda/freedom-to-minimize-dependencies-remix

- Remixは薄いフレームワーク
- Remix Way（Remixの推奨する方法）に乗る選択肢は間違いではない
- ただ、Remixと疎結合にする選択肢も取れる
  - 参考: [React / Remix への依存を最小にするフロントエンド設計](https://user-first.ikyu.co.jp/entry/2024/08/05/142626)
- 以下のように、余計なことをしないフレームワークだからこそ、疎結合に使う選択肢が取れる
  - Web標準
  - 最小限の抽象化
  - Escape Hatch
- 将来に選択肢（自由度）を残す上でRemixはよい
  - Remixは間口が広い
    - 特殊なユースケースでも受け止めてくれる
  - 痒いところに手が届くようEscape Hatchが各所に用意されている

### 向こう1年どうなる？

- これまでのRemixはReact Routerになる
- Remix v3 = React Router v7
  - Remixの次バージョンであるv3はReact Router v7という名前になる
- 大きな変革の予感..
  - React19とRSCにより、Remixの基本概念が劇的に変わる可能性
  - 新API"Reverb"開発中: 現行版とは大きく異なるアプローチ
  - Remixの名前とコミュニティは維持
  - 近い将来革新的な新APIを公開予定
    - 参考: https://remix.run/blog/incremental-path-to-react-19#rsc-changes-remix

## Q&A

- Remixの運用におけるツラミはありますか？
  - 自由度が高いので、様々な書き方が混在してしまう..
- 今後も使い続ける予定ですか？
  - そもそもReact含めて読めないところはある
  - Serverまで行かなくても..

### 感想

- Web標準にしたがっている点、フロントエンドで特定の技術に依存しすぎない技術選定ができるのは大きなメリットだなと感じた
- RemixがReact Routerに統合されるのは知らなかった...
  - https://remix.run/blog/merging-remix-and-react-router
- 今後一年は大きな変化がありそうなので、今採用するのは危険か？
- あと、(Remixとは関係ないけど)一休の技術選定として、あえて多様性を持たせるようにしているのは新鮮だった
  - 確かに様々な技術に分散投資できるメリットはあるけど、キャッチアップとかはどうしているのか気になる
  - 基本チームごとに技術選定やアーキテクチャは任せているらしいから、そこまで問題にならないのか？
  - この前のイベントでのDMMもそうだけど、チームごとに技術選定やアーキテクチャ設計の権限を完全に委譲している会社は多いのかもしれない
