# Codex Workspace Standard

このディレクトリは、VS Code と Codex の連携運用を標準化するためのひな型です。以下の構成で、Gemini File Search Tool のワークフロー、Kiro（Specs/Agent Hooks/Steering/MCP）、Amazon Q Developerカスタマイズ、Copilot指示書、Qiitaで紹介されていた設計ドキュメント・品質ルールをCodex向けにまとめています。

## 構成
- `prompts/` — Codexに渡す定型プロンプト集（File Searchモード／タスクブリーフなど）。
- `rules/` — Codexとの協働時に必須の遵守ルールや作業手順。
- `templates/` — Specs/Agent Hooks/Steering/MCP、Amazon Qコンテキスト、Copilot指示書などをCodexで再利用できるテンプレート。

## 運用フロー
1. VS Codeで `三菱iQ-R標準ソフトVer1.510_BaseSoft.code-workspace` を開く。
2. 作業開始時に `prompts/file_search_mode.md` をCodexに渡し、ファイル検索・引用のスタンスをセットする。
3. `prompts/task_brief_template.md` をもとに今回のタスクブリーフを作成し、参照必須ファイルやルールをリスト化してCodexへ貼り付ける。
4. 要件や実装内容を `templates/specs_template.md` に沿って整理し、Codexへ共有する。
5. 自動化ルールや作業ガードレールを `templates/agent_hooks_playbook.md` と `rules/codex_operating_rules.md` から選んで指示する。
6. Amazon Q Developer や GitHub Copilot を併用する場合は `templates/amazon_q_best_practices.md` と `templates/copilot_instructions_template.md` を読み込み、各エージェントに同じルールを共有する。
7. 外部情報参照やAPI連携が必要な場合は `templates/mcp_setup_guide.md` を参照し、Codexへ必要な接続情報を渡す。
8. ドキュメント資産の棚卸しやジュニアエンジニアの支援は `templates/design_docs_roles.md`、`rules/common_quality_rules.md`、`rules/junior_manager_checklist.md` を利用する。

## Codexへの指示テンプレ最適化
1. **タスクブリーフを先に作る** — `prompts/task_brief_template.md` に沿って「前提 / 必須参照ファイル / ルール / 完了条件」を整理し、メッセージに貼り付ける。
2. **参照パスは箇条書きで** — `codex_workspace_standard/rules/*.md` や `templates/*.md` をパス付きで列挙し、「これらを必ず読んで作業して」と明記する。
3. **Hooks/テストの明示** — どのフックを有効化するか、どのテストコマンドを実行するかをブリーフ内に書いておくと抜け漏れが減る。
4. **エージェント共通化** — Codexに渡したブリーフをそのまま Amazon Q や Copilot にも渡し、`.amazonq/` や `.github/copilot-instructions.md` と整合させる。
5. **記録を残す** — 完了後は該当テンプレート（`templates/vscode_standard.md`、`templates/progress-report.md` 等）に沿って結果を記録し、次回以降の指示テンプレ更新に活かす。

## 製品開発での補足ルール
- **SBOM管理**: IEC 62443 に準拠し、使用するOSSのバージョン／ライセンスをSBOMとして作成・更新する。CodexにはSBOMの出力先とフォーマットを明示する。
- **段階的開発**: PoC → Pilot → 実機テスト（負荷/セキュリティ含む）→ 製品初版の順で進め、各段階専用ブランチを作成。成果品のみ `main` へ統合する。
- **Pilot以降のセキュリティ設計**: Pilot段階からIEC 62443に沿ったセキュリティ設計レビューと実装を必須化する。
- **負荷テスト自動化**: 実機テストフェーズでは自動負荷テストプログラムとレポート生成を要求し、ハード側の動作条件・推奨値を明記する。
- **ドキュメント整備**: ユーザー向けマニュアルに加え、開発・運用オペレーター向けマニュアルも作成し、Codexへの指示で対象読者を指定する。
- **保守性/マイクロサービス設計**: 設計テンプレートでは保守性・マイクロサービス化前提を意識し、`templates/specs_template.md` や `steering_guide.md` へ反映する。

> **メモ:** すべてMarkdownなので、自分の環境に合わせて追記・派生を作ってからCodexへ貼り付けてください。
