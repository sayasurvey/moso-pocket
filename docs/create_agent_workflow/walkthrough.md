# 開発完了報告 (Walkthrough)

ご要望いただいた「moso-pocket（妄想アイデア投稿サービス）」開発用の、AIエージェント向け指示書一式の作成が完了しました。

## 作成したファイル

以下のファイルを作成し、プロジェクト内の `docs/create_agent_workflow/` ディレクトリに保存しました。
また、ご指定のルールに従い、本チャットで生成した各種管理ドキュメント（`task.md`, `implementation_plan.md`, `walkthrough.md`）も同ディレクトリにコピーしています。

1. **[agent_instructions.md](file:///Users/yona/Desktop/moso-pocket/docs/create_agent_workflow/agent_instructions.md)**
   - エージェントの役割（フルスタックエンジニア）、自律的な提案、コスト意識、セキュリティ保護などの基本指針を定義。
2. **[skills.md](file:///Users/yona/Desktop/moso-pocket/docs/create_agent_workflow/skills.md)**
   - Next.js, Lambda, API Gateway, S3, Firebase Auth, Dockerなどの技術スタック要件を定義。
3. **[rules.md](file:///Users/yona/Desktop/moso-pocket/docs/create_agent_workflow/rules.md)**
   - 従量課金制の徹底、個人情報の非保持（ニックネーム運用）、最新パッケージの利用、Dockerによる環境構築のルール。
4. **[workflow.md](file:///Users/yona/Desktop/moso-pocket/docs/create_agent_workflow/workflow.md)**
   - Docker環境の構築から、認証、DB設計、API連携、フロントエンド統合までのステップバイステップ手順。

## 使い方・確認手順

1. **エージェントへの組み込み:**
   - Cursorを使用している場合：プロジェクト直下の `.cursorrules` にこれらの内容を統合するか、チャットのSystem Promptとして読み込ませてください。
   - OpenAI GPTsやその他のエージェントプラットフォームを使用している場合：`agent_instructions.md` を中心にベースプロンプトとし、必要に応じてSkillsやRulesを含めてください。
   - 実際の開発開始時は、`workflow.md` のStep 1から順番に実行するようエージェントに指示を出してください。

2. **ディレクトリの確認:**
   - ターミナルまたはエクスプローラーから `/Users/yona/Desktop/moso-pocket/docs/create_agent_workflow/` を開き、ファイルが正しく生成されていることを確認してください。

以上で、エージェントが開発をスムーズかつ安全（セキュリティリスク低減）に行うための準備が整いました。
