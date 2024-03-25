## Socket Modeについて

ソケットモードは、パブリックなHTTPリクエストURLを公開することなく、あなたのアプリがイベントAPIとインタラクティブ機能を使用できるようにします。

公開エンドポイントにペイロードを送信する代わりに、SlackはWebSocket URLを使用してアプリと通信します。WebSocketは、低レイテンシで双方向のステートフルなプロトコルを使用して、2つの当事者（この場合はSlackとあなたのアプリ）間で通信します。

パブリックHTTPエンドポイントとは異なり、あなたがリッスンするWebSocket URLは静的ではありません。URLは実行時にapps.connection.openメソッドを呼び出すことで作成され、定期的に更新されます。

ソケットモードは、企業のファイアウォールの内側で作業している開発者や、静的な HTTP エンドポイントを公開できない他のセキュリティ上の懸念がある開発者を支援します。

直接HTTPエンドポイントとソケット・モードは、アプリのコンフィグでいつでも切り替えることができます。

ソケット・モードの詳細を処理するには、当社のJava、Javascript、Python用のBoltフレームワークまたはSDKを使用することをお勧めします。プロセスが合理化され、当社のSDKの他のすべての快適な機能にアクセスできます。

参考: https://api.slack.com/apis/connections/socket

## 以下のエラーの対処法

```shell
Unhandled request ({'type': 'event_callback', 'event': {'type': 'app_mention'}})
---
[Suggestion] You can handle this type of event with the following listener function:

@app.event("app_mention")
def handle_app_mention_events(body, logger):
    logger.info(body)
```

`SocketModeHandler(app, os.environ["SLACK_APP_TOKEN"]).start()`よりも上で関数は定義しないといけないらしい。

参考: https://github.com/slackapi/bolt-python/issues/562#issuecomment-1005221746

