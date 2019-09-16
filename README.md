# Portfolio01

### サービス名
- AwesomeMusic

### 概要
- おすすめ音楽投稿&共有サービス

### 主な機能
- おすすめ音楽新規投稿機能(タイトル、YoutubeURL、メッセージ)
- 投稿へのタグ付け機能(多対多の紐付け)
- 投稿へのコメント機能
- ユーザー一覧機能
- タグ一覧機能
- ユーザー一覧機能
- 部分一致検索機能(投稿タイトル、ユーザー名、タグ名)
- Youtube音声ストリーミング機能
- SPAフロントエンド+バックエンドAPI構成

### ソース
- フロントエンド
  - https://github.com/oshou/AwesomeMusic-front
- バックエンドAPI
  - https://github.com/oshou/AwesomeMusic-api
- DB
  - https://github.com/oshou/AwesomeMusic-db
- インフラ
  - https://github.com/oshou/AwesomeMusic-k8s

### 選択技術
- フロントエンド
  - 概要: Nuxt.jsによるフロントエンドSPA
  - 言語: Node v10
  - F/W: Nuxt.js
  - ライブラリ管理: yarn
  - 状態管理: Vuex
  - 実行環境: Dockerコンテナ(node:10-alpine)
  - UI-F/W: uikit
  - APIクライアント: axios
  - 開発環境: docker-compose

- バックエンドAPI
  - 概要: GolangによるバックエンドREST API
  - 言語: Golang v1.11
  - F/W: Gin
  - ORM: Gorm
  - ライブラリ管理: GoModule
  - 環境変数管理: godotenv
  - 実行環境: Dockerコンテナ(scratch)
  - 開発環境: docker-compose
  - APIテスト: Postman
  - タスクランナー: Make

- DB
  - 概要: 投稿データ等保管用のDBコンテナ定義、初期SQL
  - DBMS: MySQL v5.7
  - 実行環境: Dockerコンテナ(scratch)
  - 開発環境: docker-compose

- インフラ
  - 概要: 各種インフラ管理用のk8sマニフェストファイル
  - PaaS: GCP + Kubernetes
  - 構成
    - f1-micro x3

- コンテナレポジトリ
  - Dockerhub Automate-build

- 監視
  - Mackerel(k8sのDaemonset運用)

### 重視した箇所
- 1ストップでインフラからフロントエンドまで実装する
- 新規チャレンジとして以下採用
  - GCP + k8s
    - 普段AWSを使用していますが、kubernetes利用にメリット
  - Nuxt.jsフロントエンド

### 今後対応予定
- Youtube無効URL判定機能
- APIのgrpc対応
- ログ分析基盤の整備
  - fluentdでサイドカーコンテナを立てBigQueryに保管
- CircleCIによるUnitTest
- パフォーマンスチューニング
- Auth0による認証基盤作成+ソーシャルログイン
- ページネーション
