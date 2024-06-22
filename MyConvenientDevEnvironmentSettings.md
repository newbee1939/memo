# 設定一覧

## Macにインストールするツール

- [Visual Studio Code](https://code.visualstudio.com/Download)
- [Homebrew](https://brew.sh/)
- [Clipy](https://clipy-app.com/)
- [Sequel Ace](https://sequel-ace.com/)
  - 参考: https://formulae.brew.sh/cask/sequel-ace
- [Docker for Mac](https://docs.docker.com/desktop/install/mac-install/)
  - もしくはRancher Desktopなどの代替ツール

## Homebrewでインストールするツール

- jq
- starship
- git
  - デフォルトでインストールされている場合は不要

これらのbrewのパッケージは、`Brewfile`を使ってインストールすることも可能。

以下のコマンドを実行する。

```shell
vim ~/.Brewfile
```

そして、以下の内容を設定する。

```
brew "jq"
brew "starship"
```

上記の設定内容は、移行元のPCで以下のコマンドを実行することで生成できる。

```shell
brew bundle dump --global
```

以下のコマンドでこれらのパッケージを一括でインストールできる。

```shell
brew bundle --global
```

一つ一つ手動でインストールしなくていいのでよい。

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
esbenp.prettier-vscode
```

このリストは、exportする側で以下のように出力できる。

```shell
code --list-extensions > extensions.list
```

参考: https://stackoverflow.com/questions/35773299/how-can-you-export-the-visual-studio-code-extension-list

2. 以下のコマンドで一括インストールする

```shell
cat extensions.list | while read extension; do code --install-extension "$extension"; done
```

- cat extensions.list コマンドは、`extensions.list` ファイルの内容を出力する。このファイルには、インストールしたいVisual Studio Codeの拡張機能のIDが行ごとに記載されている
- | はパイプと呼ばれ、左側のコマンドの出力を右側のコマンドの入力として渡す
- while read extension は、パイプから渡された出力（この場合は`extensions.list`の内容）を1行ずつ読み込むループを作成する。`read extension` は、読み込んだ行を変数`extension`に格納する
- do code --install-extension "$extension" は、`while`ループの本体で、`code --install-extension` コマンドを使用して、変数`extension`に格納された拡張機能IDをインストールする
- done は、`while`ループの終わりを示す

### settings.jsonの設定

1. `Cmd + Shift + P`でコマンドパレットを開く
2. `user settings`と入力し、`Preferences: Open User Settings（JSON）`をクリック
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
  "workbench.editor.showTabs": "none",
  "editor.minimap.enabled": false,
  "workbench.statusBar.visible": false,
  "window.customTitleBarVisibility": "windowed",
  "editor.glyphMargin": false,
  "editor.folding": false,
  "workbench.iconTheme": "material-icon-theme",
  "breadcrumbs.symbolPath": "off",
  "workbench.activityBar.location": "top",
}
```

## Shell・ターミナルの設定

### gitのユーザー&エイリアス設定

# 参考

- [現役Web系エンジニアのMac開発環境を公開します！](https://www.engilaboo.com/my-pc-settings/)
- [最小限の手順でTypeScriptが動作する環境を構築する](https://www.engilaboo.com/build-environment-of-typescript/)
- [現役Web系エンジニアが使っているツールとMac設定を公開します【仕事の効率UP】](https://www.engilaboo.com/my-mac-settings/)

# 備考

- 常にブラッシュアップ
- いかにサボるか

# TODO

- 全て自動化したい
- Automatorとか使えない？Macの