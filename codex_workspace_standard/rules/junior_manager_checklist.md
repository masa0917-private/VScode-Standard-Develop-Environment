# ジュニアエンジニア向け Codex マネジメントチェックリスト
Qiita (tomada) 記事で紹介されていた「AIエージェントを迷わせないための設計資産」を、ジュニアエンジニアでも回せるようチェックリスト化しました。

## 事前準備
- [ ] `specs/` に機能ごとの Requirements/Design/Tasks を作成し、Codexにリンクを共有した。
- [ ] `01_development_docs` の該当ドキュメント（Architecture、API、Error Handling等）を読み、変更差分がないことを確認した。
- [ ] `codex_workspace_standard/prompts/file_search_mode.md` をCodexに読み込ませ、引用ルールを理解させた。
- [ ] `prompts/task_brief_template.md` を埋め、参照ファイル/ルール/完了条件を事前に共有した。
- [ ] `.github/copilot-instructions.md` / `.amazonq/` を `templates/copilot_instructions_template.md` / `templates/amazon_q_best_practices.md` に従って更新済みか確認した。

## 作業依頼時
- [ ] 依頼する範囲とスコープ外を明記（例: DB変更は不可）。
- [ ] 必須参照ドキュメントを列挙し、ファイルパスと目的を伝えた。
- [ ] テスト/レビュー観点を `09_test_strategy.md` と `rules/common_quality_rules.md` から引用し、完了条件に含めた。
- [ ] 言語ルール（英語思考→日本語出力）と Docker Compose v2 遵守を明記した。

## 進行中
- [ ] Codexが行った`rg`/`python`等の検索内容を確認し、根拠のない推測がないかチェック。
- [ ] Hooks（format/test/security）が有効かトレース。必要なら再適用を依頼。
- [ ] MCPを使う操作（GitHub Issue作成など）は、実行前に内容を確認した。

## 完了判定
- [ ] 変更ファイルにすべて引用が付いているか。
- [ ] Specsのタスクリストにチェックを入れ、何を完了したか明文化した。
- [ ] `design_docs_roles.md` 該当章・`.github/copilot-instructions.md`・`.amazonq/rules` の更新有無を記録し、必要なら追記した。
- [ ] 学びや注意点を `docs/notes/junior_handover.md` 等に追記し、次回以降の指針にした。

> このチェックリストを使うことで、ジュニアメンバーでもCodexを「マネジ」でき、自律的に品質を担保できます。
