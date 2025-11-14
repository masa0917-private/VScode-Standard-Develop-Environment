# Codex Task Brief Template
> VS Codeでタスクをアサインするたびに、このテンプレへ内容を埋めてCodexへ貼り付けることで、ルールと参照ファイルを確実に共有できます。

## 1. セッション前提
- リポジトリ / ワークスペース:
- タスク概要:
- スコープ外:
- 開発段階 (PoC / Pilot / 実機テスト / 製品初版):
- 関連ブランチ (段階ごとに専用ブランチを作成し、完了後にmainへ統合):

## 2. 必須参照ファイル
1. `codex_workspace_standard/rules/common_quality_rules.md`
2. `codex_workspace_standard/rules/codex_operating_rules.md`
3. （例）`docs/specs/<feature>/requirements.md`
4. （必要に応じて追加）

> **指示例**: 「上記ファイルを読み、引用付きで回答してください。」

## 3. ルール / プロンプト
- 言語ルール: 英語で思考 → 日本語で出力（ファイル生成・Gitメッセージ含む）
- File Searchモード: `prompts/file_search_mode.md`
- 追加で強調したいガードレール:
- IEC 62443 / セキュリティ: （Pilot以降は必ずセキュリティ設計・評価を含める）
- SBOM / OSS管理: （SBOMの更新方法や出力先を明記）

## 4. Hooks / テスト / コマンド
- Hooks: `auto-format-on-save`, `test-generator`, `security-scanner` など
- テスト: `npm run test`, `pytest`, `plc_unit_test`, …
- 負荷テスト（自動化）: 使用するスクリプト / ツール / レポート出力先
- その他必須コマンド: `docker compose config`, `python3 scripts/...`

## 5. 成果物と完了条件
- 期待するファイル・差分:
- レポート形式（例: `templates/progress-report.md` を使用）:
- レビュー観点:
- マニュアル: ユーザー向け / オペレーター向け
- SBOM・セキュリティ・負荷テストレポートの提出有無

## 6. 共有/追記メモ
- Codexで得た知見をどこに残すか（例: `docs/notes/<date>.md`）
- 次のセッションへ引き継ぐべき注意点
