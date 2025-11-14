# 技術設計ドキュメント15種の役割テンプレ
Qiita (tomada) 記事で紹介されていた `.claude/01_development_docs` の考え方を、Codex向けに汎用化しました。プロジェクト開始時に以下のファイルを用意し、Codexへ参照パスを共有してください。

| ファイル | 目的 / 入れる内容 | Codexへの指示例 |
|----------|------------------|----------------|
| `01_architecture_design.md` | DDD/クリーンアーキなど、レイヤ責務・依存ルール。 | 「ビジネスロジックは domain、IOは infrastructure。設計書1章を参照」 |
| `02_database_design.md` | ER図、カラム命名規則、インデックス方針、FK制約。 | 「`docs/.../02_database_design.md` に従ってマイグレーション生成」 |
| `03_api_design.md` | REST/GraphQL等のエンドポイント定義、成功/エラーのJSON形。 | 「APIレスポンスは 03 の `standard_response` セクションを必ず守る」 |
| `04_screen_transition_design.md` | 画面遷移、有効な導線、アクセス権。 | 「HMI遷移は 04 のテーブルを基に。」 |
| `05_seo_requirements.md` | メタタグ、構造化データ、サイトマップ運用。 | 「SEO設定を05章の checklist で検証して」 |
| `06_error_handling_design.md` | エラー分類、ログレベル、ユーザー表示ポリシー。 | 「例外設計は06を参照、ログ分類を外さないこと」 |
| `07_type_definitions.md` | 共通ドメイン型、APIレスポンス型、フォーム型。 | 「新しい型は 07 の naming rules に沿う」 |
| `08_development_setup.md` | ツール/SDKのセットアップ、環境変数、初期データ。 | 「環境構築は08参照、`npm run setup` を自動化」 |
| `09_test_strategy.md` | 単体/統合/E2Eの比率、TDDルール、カバレッジ目標。 | 「テスト増強は09章 scenario matrix を反映」 |
| `10_frontend_design.md` | コンポーネント分類、props設計、状態管理、スタイリング。 | 「UI作成時は10のcomponent taxonomyを守る」 |
| `11_cicd_design.md` | CI/CDパイプライン、品質ゲート、デプロイ手順。 | 「CIジョブは11章 pipeline_rundown に追加」 |
| `12_e2e_test_design.md` | クリティカルフロー、テストデータ、ブラウザマトリクス。 | 「E2Eは12のcritical_path.xlsxに沿って書く」 |
| `13_security_design.md` | 認証/認可、入力検証、秘密情報、監査ログ。 | 「秘密情報は13のSecret Policy section従って対応」 |
| `14_performance_optimization.md` | キャッシュ、画像/アセット最適化、Core Web Vitals目標。 | 「性能追加時は14のbudget表を参照」 |
| `15_performance_monitoring.md` | 計測指標、監視ツール、アラート閾値。 | 「計測タグは15章 instrumentation list に沿う」 |

## 使い方
1. それぞれのMarkdownを `docs/architecture/...` 等に保存。
2. Codexに「該当セクションを参照して実装/レビューして」と伝える。
3. 変更が入ったら `rules/junior_manager_checklist.md` を使い、ジュニアメンバーでも追従できるよう更新履歴をまとめる。
