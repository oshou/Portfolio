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
- SPAフロントエンドによるUX向上
- バックエンドREST API

### ソース
- インフラ(Kubernetes)
  - https://github.com/oshou/AwesomeMusic-k8s
- DB
  - https://github.com/oshou/AwesomeMusic-db
- バックエンドAPI
  - https://github.com/oshou/AwesomeMusic-api
- フロントエンド
  - https://github.com/oshou/AwesomeMusic-front

### 選択技術
- インフラ
  - 概要: 各種インフラ管理用のk8sマニフェストファイル
  - オンプレ環境
    - GKE + Kubernetes
    - f1-micro x3
  - ローカル環境
    - minikube

- DB
  - 概要: 投稿データ等保管用のDBコンテナ定義、初期SQL
  - DBMS: MySQL v5.7
  - 実行環境: Dockerコンテナ(debian-mysql5.7)
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

- フロントエンド
  - 概要: Nuxt.jsによるフロントエンドSPA
  - 言語: Node v10
  - F/W: Nuxt.js
  - ライブラリ管理: yarn
  - 状態管理: Vuex
  - 実行環境: Dockerコンテナ(node:10-alpine)
  - 開発環境: docker-compose
  - UI-F/W: uikit
  - APIクライアント: axios

- コンテナレジストリ
  - Dockerhub

- 監視
  - Mackerel(k8sのDaemonset運用)

### 重視した箇所
- 1ストップでインフラからフロントエンドまで実装する
- 新規チャレンジとして以下採用
  - GCP + k8s
    - 普段AWSを使用していますが、kubernetes利用にメリット
  - Nuxt.jsフロントエンド


## 画面イメージ
- 投稿一覧
![投稿一覧](https://github.com/oshou/Portfolio/portfolio01/img/post_summary.png)

- タグ一覧
![タグ一覧](https://github.com/oshou/Portfolio/portfolio01/img/tag_summary.png)

- ユーザー一覧
![ユーザー一覧](https://github.com/oshou/Portfolio/portfolio01/img/user_summary.png)

- コメント一覧
![コメント一覧](https://github.com/oshou/Portfolio/portfolio01/img/comment_summary.png)

- 検索機能
  - 投稿タイトル
![検索機能(投稿タイトル)](https://github.com/oshou/Portfolio/portfolio01/img/search_post_title.png)
  - タグ名
![検索機能(タグ名)](https://github.com/oshou/Portfolio/portfolio01/img/search_tag_name.png)
  - ユーザー名
![検索機能(ユーザー名)](https://github.com/oshou/Portfolio/portfolio01/img/search_user_name.png)

- GCP構成
![GCP構成](https://github.com/oshou/Portfolio/portfolio01/img/search_user_name.png)

- Mackerel監視
![Mackerel監視画面](https://github.com/oshou/Portfolio/portfolio01/img/search_user_name.png)


### 今後対応予定
- Auth0による認証基盤作成+ソーシャルログイン
- Youtube無効URL判定機能
- ログ分析基盤の整備
  - サイドカーコンテナでfluentd立ててBigQueryに保管
- CircleCIによるUnitTest
- パフォーマンスチューニング
  - クエリチューニング
  - APIのGRPC対応等
