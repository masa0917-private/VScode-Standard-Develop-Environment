# MCP Setup Guide (Model Context Protocol)
Kiroの記事をベースに、CodexでMCPサーバーを扱うときのテンプレ化した手順です。

## 1. 設定ファイル例 (`.codex/mcp.json`)
```json
{
  "mcpServers": {
    "aws-docs": {
      "command": "uvx",
      "args": ["awslabs.aws-documentation-mcp-server@latest"],
      "env": {
        "FASTMCP_LOG_LEVEL": "ERROR"
      },
      "autoApprove": [
        "mcp_aws_docs_search_documentation",
        "mcp_aws_docs_read_documentation"
      ]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "$GITHUB_TOKEN"
      },
      "timeout": 10000,
      "trust": false
    }
  }
}
```

## 2. 主要サーバーの使いどころ
- **AWS Documentation**: S3/Lambda/DynamoDB等の公式ドキュメント検索を自動化。`aws-docs`タグ付きの応答は根拠リンク付き。
- **GitHub**: リポジトリのIssue/PR作成やコード検索。個人アクセストークン（`repo`, `user`権限）を環境変数に入れる。
- **Custom (社内API)**: Node/PythonでRESTクライアントを公開し、`search_company_docs`, `get_employee_info` のように JSON Schema でパラメータを定義する。

## 3. テスト & トラブルシュート
1. `Codex CLI > MCP Logs`（`logs/mcp.log`など）で起動メッセージとエラーを確認。
2. `npx @modelcontextprotocol/client send` を使って手動で `list_tools` / `call_tool` を叩き、スキーマが正しいか検証。
3. タイムアウト時は `timeout` を延長する前にネットワーク/認証/argsを再確認。
4. 失敗したツールは `autoApprove` せず、ユーザー承認フローを挟む。

## 4. Codexへの伝え方テンプレ
```
MCP servers loaded:
- aws-docs: uvx awslabs.aws-documentation-mcp-server@latest (auto approve search/read)
- github: npx -y @modelcontextprotocol/server-github (token=$GITHUB_TOKEN, timeout 10s)
Use them whenever you need official AWS docs or GitHub metadata.
```

## 5. 運用フック
- サーバー追加時は `codex_workspace_standard/templates/mcp_setup_guide.md` を更新し、PRで共有。
- `.env` に秘密鍵を入れ、`rules/codex_operating_rules.md` で秘匿ポリシーを必ず参照させる。
