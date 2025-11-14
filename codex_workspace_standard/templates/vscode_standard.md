# VS Code 標準フォーマット
このテンプレを `.vscode/codex-standard.md` 等として共有すると、ワークスペースに参加する人が迷いません。

## 1. ワークスペース設定
- `三菱iQ-R標準ソフトVer1.510_BaseSoft.code-workspace` を開く。
- 重要設定
  - `files.exclude`: `.git`, `.DS_Store`, `node_modules` を非表示。
  - `search.exclude`: `.git`, `.idea`。
  - `terminal.integrated.cwd`: `${workspaceFolder}`。
- 拡張推奨: GitLens, Markdown All in One, ESLint/Prettier, PLC Editor, Amazon Q Developer, GitHub Copilot Chat。

## 2. 起動時シーケンス
1. `codex_workspace_standard/prompts/file_search_mode.md` をCodexに貼り付けてFile Searchモードを開始。
2. `templates/steering_guide.md` のペルソナ/技術スタックを読み直してから作業を開始。
3. `.github/copilot-instructions.md` と `.amazonq/` を `templates/copilot_instructions_template.md` と `templates/amazon_q_best_practices.md` に沿って最新化し、必要に応じて `/context` 指示で読み込ませる。
4. `rules/common_quality_rules.md` で「英語で思考し日本語で出力」「Docker Compose v2 を使う」などの必須ルールを確認し、タスクブリーフに明記する。
5. 作業対象フィーチャーの `specs/<feature>/` を確認。

## 3. Codexへの渡し方テンプレ
```
開いているworkspace: iQ-R BaseSoft
参照してほしいドキュメント:
- codex_workspace_standard/templates/specs_template.md
- codex_workspace_standard/templates/design_docs_roles.md
- codex_workspace_standard/templates/amazon_q_best_practices.md
- codex_workspace_standard/templates/copilot_instructions_template.md
- codex_workspace_standard/rules/common_quality_rules.md
Hooks: auto-format-on-save, test-generator, security-scanner
Amazon Q / Copilot context: README.md, amazonQ.md, .amazonq/rules/coding/*.md, .github/copilot-instructions.md
```

## 4. 終了時チェック
- `git status` または差分管理ツールで未コミットを確認。
- `rules/codex_operating_rules.md` と `rules/common_quality_rules.md` の手順に沿って引用・根拠付きでレビュー。
- `.github/copilot-instructions.md` や `.amazonq/rules` に差分があれば必ずコミットメッセージに含める。
- 必要に応じてMCPサーバーのログを確認し、`logs/mcp.log` をクリーンアップ。
