## 検証用リポジトリ

https://github.com/newbee1939/wasbook-docker

## ボットネットワーク

- ボットとはマルウェアの一種で、外部からの指令を受けて、迷惑メール送信やDDos攻撃などの不正活動を行うもの
- 現役の攻撃手法の一つ

## 脆弱性が生まれる理由

- バグによるもの
- チェック機能の不足によるもの

## セキュリティガイドライン

- 安全なウェブサイトの作り方
    - https://www.ipa.go.jp/security/vuln/websecurity/about.html
- OWASP Top 10
    - https://owasp.org/Top10/ja/
    - Webアプリの最も重大なリスクのトップ10

## OWASP ZAPとは

- OWASP ZAP（OWASP Zed Attack Proxy）は、Webアプリケーション脆弱性診断用ツール
- OWASP ZAPはPC上でプロキシとして動作し、HTTP通信を観察したり、変更したりすることができる

## HTTP: レスポンスヘッダ

- 代表的なヘッダ
    - Content-Length
        - ボディのバイト数
    - Content-Type
        - `MIMEタイプ`というリソースの種類を指定
        - 以下のようなMIMEタイプがある
            - text/plain
            - image/gif
            - application/pdf

## Cookie: セキュリティを担保するためのセッションIDの要件

下記を守らないとなりすましが行われる可能性がある。

- 第三者がセッションIDを推測できないこと
- 第三者からセッションIDを強制されないこと
- 第三者にセッションIDが漏洩しないこと