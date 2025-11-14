# Codex Operating Rules
Codexと共同作業するときの必須ルールです。

1. **言語と出力** — 英語で思考し、日本語で回答・ファイル生成・Gitコミットメッセージを作成する。違反した場合は出力をやり直す。
2. **File Searchモード徹底** — `prompts/file_search_mode.md` を読み込ませ、すべての回答に `path:line` 形式の引用を付ける。Gemini File Search Tool同様に、根拠のない回答は禁止。
3. **Specs優先** — 作業前に `templates/specs_template.md` で要件/設計/タスクを整え、Codexにパスを明示する。曖昧な指示は禁止。
4. **Hooksで品質を自動化** — 保存・新規作成・レビュー前など、`agent_hooks_playbook.md` から該当フックを選んで事前に宣言する。
5. **Steeringを更新** — プロジェクトの背景/技術/構造が変わったら即 `steering_guide.md` の項目を更新し、Codexに最新ファイルのパスを伝える。
6. **MCPの責務分離** — AWSドキュメント検索やGitHub操作は `mcp_setup_guide.md` の設定情報を参照。環境変数やトークンはチャットに貼らない。
7. **設計ドキュメントの連鎖** — 15種の設計ドキュメントに変更が入るときは、関連ファイルを表形式で列挙し、Codexに更新対象をレビューさせる。
8. **秘匿情報の扱い** — `agent_hooks_playbook.md` の `security-scanner` を走らせた後でしかコミット/提出しない。共有時はマスク。
9. **ジュニア支援** — 作業手順は `rules/junior_manager_checklist.md` のチェックリスト形式でまとめ、Codexに参照させることでジュニアエンジニアでも判断できるようにする。
10. **Docker Compose v2 遵守** — `docker compose` CLI だけを使用し、旧 `docker-compose` コマンドを呼び出さない。更新時は `templates/vscode_standard.md` と `templates/amazon_q_best_practices.md` を参照。
11. **開発フェーズ管理** — PoC / Pilot / 実機テスト / 製品初版の段階ごとにブランチを分け、タスクブリーフへ段階とゴール、必要なマニュアル・SBOM更新を必ず記載する。
12. **Copilot / Amazon Q 同期** — `.github/copilot-instructions.md` と `.amazonq/` のルールが `rules/common_quality_rules.md` と矛盾しないか確認し、同じ指示をCodex・Copilot・Amazon Qへ共有する。
