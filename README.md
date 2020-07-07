# ポートフォリオ#01

### サービス名
- AwesomeMusic

### 概要
- お勧め音楽投稿&共有サービス

### 主な機能
- お勧め音楽新規投稿(タイトル、YoutubeURL、メッセージ)
- 投稿へのタグ付け(多対多の紐付け)
- 投稿へのコメント
- 投稿一覧表示
- ユーザー一覧表示
- タグ一覧表示
- 部分一致検索(投稿タイトル、ユーザー名、タグ名)
- Youtube音声ストリーミング
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

### 構成要素毎の概要
- インフラ
  - 概要: 各種インフラ管理用のk8sマニフェストファイル
  - クラウド動作環境
    - GKE + Kubernetes
    - f1-micro x3
  - ローカル動作確認環境
    - minikube, Docker for mac

- DB
  - 概要: 投稿データ等保管用のDBコンテナ定義、DDL、初期投入データ等
  - DBMS: MySQL v5.7
  - 実行環境: Dockerコンテナ(debian-mysql5.7)
  - 開発環境: docker-compose

- バックエンドAPI
  - 概要: GolangによるバックエンドREST API
  - アーキテクチャ: DDD(Onion-Architecture風)
  - 言語: Golang v1.11
  - DI: 自前Injector
  - Router: chi
  - ORM: sqlx
  - ライブラリ管理: Go Module
  - 環境変数管理: godotenv
  - 実行環境: Dockerコンテナ(scratch)
  - 開発環境: docker-compose
  - Linter: golangci-lint(lint,vet,unused...)
  - 単体テスト: testing, httptest, golang/mock(gomock, mockgen)
  - APIテスト: Postman
  - タスクランナー: Make
  - コンテナイメージ管理: skaffold
  - DBマイグレーション: sql-migrate
  - CI/CD: CircleCI / GithubAction

- フロントエンド
  - 概要: Nuxt.jsによるフロントエンドSPA
  - 言語: Node v10
  - F/W: Nuxt.js
  - ライブラリ管理: yarn
  - 実行環境: Dockerコンテナ(node:10-alpine)
  - 開発環境: docker-compose
  - 状態管理: Vuex
  - UI-F/W: uikit
  - APIクライアント: axios

- コンテナレジストリ
  - Dockerhub

- 監視
  - Mackerel(k8sのDaemonset運用)

### 作成にあたり重視したポイント
- インフラからフロントまで一気通貫で自前実装する
  - フロー理解のため
- GolangのバックエンドAPIを実装する
  - microserviceバックエンドでの利用機会が多いと思われるため
- アーキテクチャ設計
  - 抽象依存で変化に強く、テストしやすい設計を検討する。
    - 例) APIサーバのデータストアをMySQL / Postgres それぞれのパターンを実装
  - Onion-Architectureを参考に保守しやすく変化に強いレイヤー構成を検討する。
- 他課題感のある分野には未経験技術を積極的に採用する
  - GKE + k8s
    - コンテナ統合管理方法の把握のため
      (現状業務でmicroserviceが増えて来ており、
       サービス数が増えるにつれ、監視や構成管理が複雑になる可能性が高いため、
       統合管理ツールのデファクトスタンダードであるk8sを把握したい)
    - k8s関連IaaSの中で、採用事例の多さ、費用感、コンテナ作成時間等からGKEを採用
  - openapiスキーマ駆動
    - api実装の効率化が可能か検証のため採用
    - 検証フェーズでフロント向けのAPIスタブサーバとして利用
    - API設計段階でスキーマファイル更新都度、ソース自動生成＆ロジック部分補足に工数がかかったため、
      実装後半は不採用
  - Nuxt.jsフロントエンド
    - フロント側の環境理解のため
      最近のモダンなF/Wの内、最も導入コストが低く、今後SSR等多目的に応用可能と思われるため採用

### 今後対応予定
- Auth0による認証基盤作成+ソーシャルログイン
- タグ自動整理(表記ゆれ等への対応)
- Youtube無効URL判定機能
- ログ分析基盤の整備
  - サイドカー形式でfluentdコンテナ立ててBigQueryに保管等
- CircleCIによるpush時自動ビルド＆デプロイ
- パフォーマンスチューニング
  - クエリチューニング
  - APIのGRPC対応等

## 画面イメージ
- 投稿一覧
![投稿一覧](https://github.com/oshou/Portfolio/blob/master/img/post_summary.png)

- タグ一覧
![タグ一覧](https://github.com/oshou/Portfolio/blob/master/img/tag_summary.png)

- ユーザー一覧
![ユーザー一覧](https://github.com/oshou/Portfolio/blob/master/img/user_summary.png)

- 検索機能(投稿タイトル)
![検索機能(投稿タイトル)](https://github.com/oshou/Portfolio/blob/master/img/search_post_title.png)

- 検索機能(タグ名)
![検索機能(タグ名)](https://github.com/oshou/Portfolio/blob/master/img/search_tag_name.png)

- 検索機能(ユーザー名)
![検索機能(ユーザー名)](https://github.com/oshou/Portfolio/blob/master/img/search_user_name.png)

- 新規投稿
![新規投稿](https://github.com/oshou/Portfolio/blob/master/img/add_post.png)

- GKE構成
![GCP構成](https://github.com/oshou/Portfolio/blob/master/img/gke_cluster.png)
