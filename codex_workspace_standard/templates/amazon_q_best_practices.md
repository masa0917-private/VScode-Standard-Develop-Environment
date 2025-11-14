# Amazon Q Developer コンテキスト & ルール テンプレ
> `[Sony]Amazon Q Developer ランチタイムセミナー第3回` の資料で紹介されていたSBN流ベストプラクティスを、Codex/VS Codeで再利用できる形に整理しました。

## 1. フォルダー構成（起動時に読むコンテキスト）
```
project-root/
├── amazonQ.md          # AI専用の技術・制約メモ（一般的なコマンド/技術制約/ワークフローなど）
├── README.md           # 人間向けプロジェクト概要（背景、セットアップ、連絡先）
└── .amazonq/
    ├── rules/          # ルールズ（コーディング規約、アクセス制限、禁止ファイル）
    └── agents/         # カスタムエージェントJSON（役割, resources, 利用可能ツール）
```
- Qを起動するカレントディレクトリ配下の相対パスで管理する。
- プロジェクトごとに必ず専用コンテキストを作る（他案件との混在は禁止）。
- ルールやREADMEは箇条書きで焦点を絞り、不要な情報は読み込ませない。

## 2. コンテキストの中身テンプレ
### `amazonQ.md`
- 一般的なCLI/ビルドコマンド（例: `npm run build`, `gxworks3 compile`）
- 技術スタックとバージョン、デバイス構成、ネットワーク制約
- プロジェクト固有の注意事項（例: 「iQ-R安全周りのFBはFB_SAFE配下のみ変更可」）

### `README.md`
- サービス概要と目標（なぜ存在するのか/誰が使うか）
- 初期セットアップ手順と環境変数の入れ方
- コンタクト（エスカレーション先）

### `.amazonq/rules/**.md`
- 回答スタイル: 言語/敬語、`path:line`での引用必須等
- コーディング規約: 命名、禁止API、例外処理方針
- アクセス/セキュリティ: 機密情報の扱い、参照禁止ファイル、公開可否
- プロジェクトごとに細かく分割し、チャットごとに必要なルールだけON/OFFできる構造にする。

### `.amazonq/agents/*.json`
```json
{
  "name": "security-guardian",
  "description": "社内標準に沿ったセキュリティレビューワークフロー",
  "resources": {
    "docs": ["docs/security/"],
    "tools": ["mcp-github", "mcp-aws-docs"]
  },
  "instructions": [
    "常に .amazonq/rules/security.md を参照",
    "顧客データには読み取り専用でアクセス"
  ]
}
```
- `resources` に教科書的ファイル群、`tools` に許可MCP/CLIを定義。
- 役割（セキュリティ専門/新人教育など）を明示して使い分ける。

## 3. 運用チェックリスト
- [ ] コンテキストは「プロジェクトを理解する上で本当に必要な情報」だけに絞る。
- [ ] ファイル/フォルダをパターン指定で `/context` に読み込ませる場合も、対象を限定する。
- [ ] ルールファイルは用途別に細分化し、アクセス制限/回答スタイル/コーディング規約を分離。
- [ ] カスタムエージェント json では、利用可能ツールと禁止操作を必ずセットで記述。
- [ ] 定期的にREADMEとamazonQ.mdを同期し、古い手順を残さない。
- [ ] 「英語思考→日本語出力」や Docker Compose v2 の遵守を `.amazonq/rules/` で明記し、Codex・Copilot と同じ表現で共有する。

## 4. Codex/VS Code での使い方
1. `codex_workspace_standard/templates/amazon_q_best_practices.md` をベースに `.amazonq` 以下を作成。
2. VS Code起動後、Amazon QやCodexに `/context amazonQ.md .amazonq/rules/**/*.md` を読み込ませる。
3. 機能ごとに必要なルールファイル/エージェントだけを明示的にONにする。
4. 仕様変更時は `amazonQ.md` → `README.md` → `.amazonq/rules` の順で更新し、Codexに差分を伝える。
