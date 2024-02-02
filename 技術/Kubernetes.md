# KubernetesのProbeについて分かりやすくまとめてみた

TODO: 記事にハンズオンも交えて分かりやすくまとめたい

## 資料
- Configure Liveness, Readiness and Startup Probes
	- https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
- Liveness Probe、Readiness ProbeおよびStartup Probeを使用する
	- https://kubernetes.io/ja/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes
- コンテナのヘルスチェック（サービス）
	- https://cloud.google.com/run/docs/configuring/healthchecks?hl=ja
- Cloud Run サービスの信頼性をヘルスチェックで向上
	- https://cloud.google.com/blog/ja/products/serverless/cloud-run-healthchecks
- Cloud Runのヘルスチェック機能を使ってみた
	- https://iret.media/72900

## Probeの概要
- Podのヘルスチェック機構のこと（Podが正常に動作しているかを判断するための機構）
- システムでは、アプリケーションの異常を検出して、即時かつ自動的に修復することが求められる
- 原則全てのサービスで導入すべき設定
- Kubernetesには以下の3つがある
	- Startup Probe
    	- コンテナアプリケーションの起動が完了したかをチェックする
    	- 起動が完了していない場合は、Liveness Probeと Readiness Probeを実行させない
    	- Liveness Probeと Readiness Probeがアプリケーションの起動に干渉することを防ぐ
		- Startup Probeが成功しない場合、コンテナは300秒後に終了し、その後はPodのrestartPolicyに従う
		- 要は、アプリケーションの起動時間が長い場合に、起動が完了するまでLiveness ProbeやReadiness Probeのチェックを遅らせるために使用する
		- 起動が遅いアプリで特に有効
	- Liveness Probe
    	- コンテナの起動状態をチェックして、指定した条件（ヘルスチェックを通す条件）にマッチしない場合はコンテナを再起動する
    	- 例えば、アプリケーション自体は起動しているが処理を継続することができない状態（デッドロックやその他の障害状態など）の場合にコンテナを自動的に再起動することができる
	- Readiness Probe（Cloud Runでは提供されていない？）
		- KubernetesはデフォルトでPod内のコンテナが起動したタイミングで（コンテナがポートをリッスンするのを待機してから）PodをServiceに紐付ける（トラフィックを送信する）
		- コンテナ起動=アプリ起動ではない
			- リクエストを受け入れ可能になる前にルーティングされる可能性がある
		- 任意の判定基準（Readiness Probe）を入れることでアプリ起動後にPodがServiceに紐付けられることを担保する
    	- 要は、Podがリクエストを受け付けられるかを判定する
    	- 設定していないと、リクエストを受け付けられる状態になる前にServiceと紐付けられてリクエストが来るためエラーになる可能性がある
		- アプリケーションが実際にトラフィックを処理する準備ができているかを確認し、準備ができるまでトラフィックを受けないようにするために重要な設定

## Probeを入れないと何が起こる？（ざっくりと）
- アプリをデプロイをしたタイミングでアプリの起動前にProbeのヘルスチェックが走ってエラーが生じる可能性
- リクエストを受け付けることができる前にServiceと紐付けられてエラーになる可能性
- デッドロックやその他の障害時にコンテナを再起動できなくてエラーが発生し続ける可能性

## ヘルスチェックの方式
- コマンドでの実行（exec）
- リクエストでの実行（httpGet）
	- 最も一般的に使われる種類のプローブ
- TCPソケットを使用した実行（tcpSocket）

## その他補足
- Readiness ProbeとLiveness Probeは同じコンテナで同時に使用可能（同一マニフェスト内に定義できる）
- 両方を同時に使用することで、「準備できていないコンテナへのトラフィックの到達を防ぐ」＋「コンテナが失敗（デッドロックなどが発生）したときの再起動」ができる

## エンドポイントには何を設定すべきか？

- DBに繋ぎにいくページが望ましい？

## Cloud RunとProbe設定

- Cloud Runでは、アプリケーションが正常に動作しているかどうかを監視する、ヘルスチェック機能が提供されている
- この機能を使用することで、サービスが正常に稼働しているかどうかを定期的に確認できる
- Cloud Runのヘルスチェック機能は、Startup ProbeとLiveness Probeの2つの方法がある
- Startup Probe -> Liveness Probe の順に実行

## Probe設定の流れ

1. HTTPエンドポイントを追加
2. ヘルスチェックを追加
- 初期遅延
	- コンテナが開始された後、最初のProbeを実行するまでの待機時間（秒）
- 期間
	- Probeを実行する期間（秒）
- 失敗しきい値
	- コンテナを失敗と判断する前にProbeを再試行する回数
- タイムアウト
	- Probeがタイムアウトするまでの待機時間（秒）	
3. ログに出力されているか確認
