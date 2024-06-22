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

- `code .`でVSCodeを開けるようにする
  1. `Cmd + Shift + P`でコマンドパレットを開く
  2. `shell` と入力し、`Shell Command: install 'code' command in PATH`を選択する


-  "workbench.editor.showTabs": "none"は入れたい
  - extensions.json
- Blockmanも良さそう
- Material Icon Theme
  "workbench.editor.showTabs": "none",
  "editor.minimap.enabled": false,
  "workbench.statusBar.visible": false
  "window.customTitleBarVisibility": "windowed"

    "editor.glyphMargin": false,
  "editor.folding": false

  https://zenn.dev/yuichi_dev/articles/2023-02-28_vscode_shortcut

  https://zenn.dev/ryuu/articles/what-zen-mode

  https://forest.watch.impress.co.jp/docs/news/1035557.html

# 参考

- [現役Web系エンジニアのMac開発環境を公開します！](https://www.engilaboo.com/my-pc-settings/)
- [最小限の手順でTypeScriptが動作する環境を構築する](https://www.engilaboo.com/build-environment-of-typescript/)
- [現役Web系エンジニアが使っているツールとMac設定を公開します【仕事の効率UP】](https://www.engilaboo.com/my-mac-settings/)

# 備考

- 常にブラッシュアップ
- いかにサボるか

# TODO

- 全て自動化したい