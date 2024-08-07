# 設定一覧

## ダウンロードするツール

- [Visual Studio Code](https://code.visualstudio.com/Download)
- [Homebrew](https://brew.sh/)
- [Clipy](https://clipy-app.com/)
- [Sequel Ace](https://sequel-ace.com/)
  - 参考: https://formulae.brew.sh/cask/sequel-ace
- [Docker for Mac](https://docs.docker.com/desktop/install/mac-install/)
  - もしくは[Rancher Desktop](https://docs.rancherdesktop.io/getting-started/installation/)などの代替ツール
- [f.lux](https://justgetflux.com/)
  - 現在の場所を入力したら、いい感じに画面の光量を調節してくれる
    - e.g. 夜間はブルーライトをカットする など
  - もしくはMacが標準で搭載している`Night Shift`を使う
  - f.luxの方が設定が豊富でブルーライトのカット効果も高い？
    - https://www.lifehacker.jp/article/170414_night_shift_flux/

## Homebrewでインストールするツール

- jq
- starship
- gh
- font-monaspace
- git
  - デフォルトでインストールされている場合は不要

※[monaspace](https://monaspace.githubnext.com/)はGitHubのフォント

これらのbrewのパッケージは、`Brewfile`を使ってインストールすることも可能。

以下のコマンドを実行する。

```shell
vim ~/.Brewfile
```

そして、以下の内容を設定する。

```
brew "jq"
brew "starship"
brew "gh"
brew "git
cask "font-monaspace"
```

上記の設定内容は、移行元のPCで以下のコマンドを実行することで生成できる。

```shell
brew bundle dump --global
```

以下のコマンドでこれらのパッケージを一括でインストールできる。

```shell
brew bundle --global
```

一つ一つ手動でインストールしなくていいので便利。

## VSCodeの設定

### `code .`でVSCodeを開けるようにする

1. `Cmd + Shift + P`でコマンドパレットを開く
2. `shell` と入力し、`Shell Command: install 'code' command in PATH`を選択する

### 拡張(extensions)をインストールする。

1. ディレクトリ内に以下の`extensions.list`を配置する

※最低限必須なものを列挙

```list
marp-team.marp-vscode
vscodevim.vim
github.copilot
github.copilot-chat
eamodio.gitlens
streetsidesoftware.code-spell-checker
exiasr.hadolint
gruntfuggly.todo-tree
yoavbls.pretty-ts-errors
github.vscode-pull-request-github
formulahendry.auto-rename-tag
shardulm94.trailing-spaces
pkief.material-icon-theme
github.github-vscode-theme
esbenp.prettier-vscode
firsttris.vscode-jest-runner
ChakrounAnas.turbo-console-log
```

このリストは、exportする側で以下のように出力できる。

```shell
code --list-extensions > extensions.list
```

参考: [How can you export the Visual Studio Code extension list?](https://stackoverflow.com/questions/35773299/how-can-you-export-the-visual-studio-code-extension-list)
参考: [Turbo Console Log](https://qiita.com/uuki99/items/f24463ff4d66243d5626)

2. 以下のコマンドで一括インストールする

```shell
cat extensions.list | while read extension; do code --install-extension "$extension"; done
```

- コマンドの解説
  - cat extensions.list コマンドは、`extensions.list` ファイルの内容を出力する。このファイルには、インストールしたいVisual Studio Codeの拡張機能のIDが行ごとに記載されている
  - | はパイプと呼ばれ、左側のコマンドの出力を右側のコマンドの入力として渡す
  - while read extension は、パイプから渡された出力（この場合は`extensions.list`の内容）を1行ずつ読み込むループを作成する。`read extension` は、読み込んだ行を変数`extension`に格納する
  - do code --install-extension "$extension" は、`while`ループの本体で、`code --install-extension` コマンドを使用して、変数`extension`に格納された拡張機能IDをインストールする
  - done は、`while`ループの終わりを示す

### settings.jsonの設定

1. `Cmd + Shift + P`でコマンドパレットを開く
2. `user settings`と入力し、`Preferences: Open User Settings（JSON）`を選択
3. 以下の内容を記述する

```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "cSpell.userWords": [
    "astro",
    "biomejs",
    "browsi",
    "browsitag",
    "clearfix",
    "cloudrun",
    "cloudsql",
    "codegen",
    "datetime",
    "deno",
    "dprint",
    "envsubst",
    "esbenp",
    "fastify",
    "fluxtag",
    "fuga",
    "gcloud",
    "googletag",
    "hoge",
    "jotai",
    "kintone",
    "kustomize",
    "laravel",
    "luxon",
    "marp",
    "memorystore",
    "nestjs",
    "qiita",
    "testid",
    "traefik",
    "urql",
    "zenn"
  ],
  "window.zoomLevel": 2,
  "github.copilot.chat.localeOverride": "ja",
  // VSCodeの不要な要素を非表示
  "workbench.editor.showTabs": "none",
  "editor.minimap.enabled": false,
  "workbench.statusBar.visible": false,
  "window.customTitleBarVisibility": "windowed",
  "editor.glyphMargin": false,
  "editor.folding": false,
  "breadcrumbs.symbolPath": "off",
  "workbench.activityBar.location": "top",
  // VSCodeのテーマなど
  "workbench.iconTheme": "material-icon-theme",
  "workbench.colorTheme": "GitHub Dark Default",
  // Turbo Console Log
  "turboConsoleLog.addSemicolonInTheEnd": true,
  "turboConsoleLog.insertEnclosingClass": false,
  "turboConsoleLog.insertEnclosingFunction": false,
  "turboConsoleLog.quote": "'",
  "turboConsoleLog.wrapLogMessage": true,
  // タブ数制限
  "workbench.editor.limit.enabled":true,
  "workbench.editor.limit.value": 3,
  // ブラケットペアの範囲を可視化
  "editor.guides.bracketPairs": "active",
  // Monaspace
  "editor.fontFamily": "Monaspace Neon",
}
```

## Shell・ターミナルの設定

Macのデフォルトシェルである`zsh`を使用。

### gitのユーザー&エイリアス設定

以下のコマンドでユーザー名とメールアドレスを設定。

```shell
git config --global user.name "Hoge Taro"
git config --global user.email sample@example.com
```

`git config --global --edit`を実行して、以下のエイリアスを設定。

```
[alias]
st = status
co = checkout
br = branch
```

参考: [Gitでalias（エイリアス）を設定する方法をサクッと解説](https://www.engilaboo.com/how-to-set-git-alias/#google_vignette)

### GitとGitHubの連携設定

[gh auth login](https://cli.github.com/manual/gh_auth_login)を実行する（sshキーの設定）

参考: [俺たちはもう GitHub のために ssh-keygen しなくていい](https://zenn.dev/lovegraph/articles/529fe37caa3f19)

### Dockerコマンドのエイリアスを設定

以下のコマンドで.zshrcを開く。

```shell
vim ~/.zshrc
```

以下の設定を追加

```
alias dc='docker compose'
```

参考: [Dockerコマンドにalias(エイリアス)を設定する方法【作業効率UP】](https://www.engilaboo.com/docker-alias/)

### Starshipの設定

.zshrcを開く。

```shell
vim ~/.zshrc
```

以下の記述を追加。

```
eval "$(starship init zsh)"
```

より細かく設定。

```shell
mkdir -p ~/.config && vim ~/.config/starship.toml
```

starship.tomlに以下の設定を追加。

```toml
[character]
success_symbol = "[❯](bold green)"
error_symbol = "[✗](bold red)"

[git_branch]
symbol = "🌱 "
style = "bold #b8d200"

[[battery.display]]
threshold = 20
style = "bold red"
[battery]
discharging_symbol = "😞 "

[git_status]
modified = "📝"
staged = '[++\($count\)](green)'
```

参考: [Starship インストール](https://starship.rs/ja-JP/guide/)

## Chrome拡張のインストール

- [OneTab](https://chromewebstore.google.com/detail/onetab/chphlpgkkbolifaimnlloiipkdnihall?hl=ja)
- [Refined GitHub](https://chromewebstore.google.com/detail/refined-github/hlepfoohegkhhmjieoechaddaejaokhf)
  - 参考: https://github.com/refined-github/refined-github/blob/main/readme.md
- [Dark Reader](https://chromewebstore.google.com/detail/dark-reader/eimadpbcbfnmbkopoojfekhnkhdbieeh?hl=ja)
- [Send to Google Tasks](https://chromewebstore.google.com/detail/send-to-google-tasks/acomfpnllcpggnclcogaiceicgljnbac)
- [AutoPagerize](https://chromewebstore.google.com/detail/autopagerize/igiofjhpmpihnifddepnpngfjhkfenbp)
- [AdBlock](https://chromewebstore.google.com/detail/adblock-%E2%80%94-%E6%9C%80%E9%AB%98%E5%B3%B0%E3%81%AE%E5%BA%83%E5%91%8A%E3%83%96%E3%83%AD%E3%83%83%E3%82%AB%E3%83%BC/gighmmpiobklfepjocnamgkkbiglidom?hl=ja)
- [Redirect Path](https://chromewebstore.google.com/detail/redirect-path/aomidfkchockcldhbkggjokdkkebmdll?hl=ja)
- [EditThisCookie](https://chromewebstore.google.com/detail/fngmhnnpilhplaeedifhccceomclgfbg?hl=ja)
- [Vimium](https://chromewebstore.google.com/detail/vimium/dbepggeogbaibhgnhhndojpepiihcmeb?hl=ja-jp)
  - 参考: [ブラウザを Vim ライクに操作する Vimium の布教と知見まとめ](https://zenn.dev/mkobayashime/articles/vimium-vim-browser)
- [ModHeader](https://chromewebstore.google.com/detail/modheader-modify-http-hea/idgpnmonknjnojddfkpgkljpfnnfcklj)
  - Akamaiを使う場合は以下のHeader情報を設定
    - `Pragma`
    - `akamai-x-cache-on,akamai-x-cache-remote-on,akamai-x-check-cacheable,akamai-x-get-cache-key,akamai-x-get-extracted-values,akamai-x-get-request-id,akamai-x-serial-no, akamai-x-get-true-cache-key`
      - 参考: [ArticlesAkamai設定の検証やデバッグ方法（Chrome編）](https://community.akamai.com/customers/s/article/Akamai-Chromerxdxn?language=en_US)
- theme(以下のいずれか)
  - [Earth View from Google Earth](https://chromewebstore.google.com/detail/earth-view-from-google-ea/bhloflhklmhfpedakmangadcdofhnnoh?hl=ja)
  - [Black & White](https://chromewebstore.google.com/detail/black-white/mhhlgkfginnlendpfkhcmldikeepoefa)
  - [Pig](https://chromewebstore.google.com/detail/pig/mkdclmahlehmldpgdkbbiipiinebleac)

## Macの設定

- よく使う言葉の辞書登録
  - ありがとうございます
  - よろしくお願いいたします
  - お疲れ様です
  - 承知しました
- キーボード操作時の音を消す
  - `System Preferences > Sound > Sound Effects`のVolumeを0に
- メニューバーを右にする
  - `System Preferences > Dock > Position on screen > Right`

# 参考

- [現役Web系エンジニアのMac開発環境を公開します！](https://www.engilaboo.com/my-pc-settings/)
- [最小限の手順でTypeScriptが動作する環境を構築する](https://www.engilaboo.com/build-environment-of-typescript/)
- [現役Web系エンジニアが使っているツールとMac設定を公開します【仕事の効率UP】](https://www.engilaboo.com/my-mac-settings/)

# 備考

- 常にブラッシュアップ
- 情報を集めて試す
- いかにサボるか
- より楽しく楽に働けるように工夫する

# TODO

- 全て自動化したい
- Automatorとか使えない？Macの
- QiitaかZennにアウトプットする
  - 「VSCodeを究極にシンプルにする」
