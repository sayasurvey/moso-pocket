# 開発ワークフロー (Workflow)

AIエージェントが「moso-pocket」を開発するためのステップバイステップの手順です。この順序に従って実装と検証を進めてください。

## Step 1: プロジェクトの初期設定・Docker環境構築
1. `service-posting-pages` ディレクトリの内容を確認し、依存関係（`package.json`）などを把握する。
2. 開発用の `Dockerfile` および `compose.yaml` を作成する。
3. パッケージ群（`nuxt`, `vue`, `firebase`, 等）が最新であることを確認し、必要ならアップデート（`pnpm up -iL` 相当）を行う。
4. Dockerコンテナを起動し、フロントエンド画面（S3デプロイ向けのクライアントサイド/SSG想定）が正常に表示されることを確認する。

## Step 2: 認証システムの実装
1. Firebase プロジェクトを作成（ユーザーによる手動操作を案内するか、CLIを利用）し、設定ファイル（`.env.local`等）に環境変数を追加する。
2. Firebase Authentication を有効化し、「Google認証」および「メールアドレス/パスワード認証」をプロジェクト内に実装する。
3. プライバシー保護ルール（ルール2）に基づき、登録時にニックネームのみを保存するユーザー管理ロジックを実装する。

## Step 3: データベース設計・バックエンド準備
1. データベース（例: Firestore または DynamoDB）の設計を行う。
   - **User Collection:** `uid`, `nickname`, `createdAt`
   - **Post Collection:** `id`, `authorUid`, `title` (概要), `target` (ターゲット), `imageUrl` (イメージ画像), `reason` (きっかけ), `createdAt`
   - **Reply Collection:** `id`, `postId`, `authorUid`, `message` (メッセージ), `serviceLink` (製品リンク), `createdAt`
2. AWS（Lambda, API Gateway, S3）を利用するためのIaC基盤（AWS SAM または Serverless Framework等）を準備する。

## Step 4: 投稿機能（API & フロントエンド連携）
1. **S3 画像アップロード:**
   - フロントエンドから直接S3に画像をアップロードできるように、Lambdaで署名付きURL（Presigned URL）を発行するAPIを作成する。
2. **投稿データの保存:**
   - 投稿内容をデータベースへ保存するLambda APIを実装し、Firebase Authのトークン検証ミドルウェアを組み込む。
3. **フロントエンドの実装:**
   - 用意されたデザインファイルのフォーム部分に、React Hook Formなどを利用してAPI連携処理を実装する。

## Step 5: 閲覧・リプライ機能（API & フロントエンド連携）
1. **一覧取得API:**
   - 投稿一覧と詳細情報を取得するAPIを作成する。
2. **リプライAPI:**
   - 投稿に対してリプライ（メッセージとリンク）を保存するAPIを作成する。
3. **フロントエンドの実装:**
   - 詳細ページでリプライを表示し、投稿できるUIにAPI呼び出しを結合する。

## Step 6: テストとデプロイ準備
1. 開発した機能全体の動作確認（E2Eテストや手動テスト）を実施する。
2. Nuxtの静的エクスポート（`nuxt generate`）を実行し、生成された静的ファイルをS3へデプロイするスクリプトやCI/CD（GitHub Actions等）の設定を行う。
