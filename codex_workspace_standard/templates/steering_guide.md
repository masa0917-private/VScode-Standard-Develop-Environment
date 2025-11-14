# Steering Guide (Project Memory Pack)
KiroのSteering機能をCodex用に落とし込んだテンプレです。`.codex/steering/` 以下に配置すると管理しやすくなります。

## 1. product.md（製品概要）
- **ミッション/タグライン:**
- **主要ユーザー / ペルソナ:**
- **ユースケース:**
- **成功指標 (KPI/KGI):**
- **禁止事項:** 例) 未認証ユーザーはXX画面にアクセス不可

## 2. tech.md（技術スタック）
| レイヤ | 採用技術 | バージョン/備考 |
|--------|----------|-----------------|
| UI/HMI |          | 例: Vue 3 + Tailwind |
| 制御   |          | 例: GX Works3, iQ-R FB |
| API    |          | REST/OPC-UA 等 |
| DB     |          |                 |
| ツール | pnpm, ESLint, Husky 等 |

- Node/言語バージョン、パッケージマネージャー強制、lint/format/testコマンドを明記。
- 監視/CI/CD/Secretsなど、AIが触れると危険な領域も明確にする。

## 3. structure.md（フォルダ構造/命名規約）
```
project-root/
├── src/
│   ├── plc/            # PLCロジック
│   ├── hmi/            # GOT/HMI資産
│   ├── scripts/        # 自動化スクリプト
│   └── tests/
├── docs/
└── codex_workspace_standard/
```
- 命名規約（PascalCase, camelCase, UPPER_SNAKE_CASE）
- UI/FB/ラダーの配置、階層化ルール
- よくある落とし穴（例: サーバ/クライアント間でクラス渡し禁止、`npm run check`前にコミット禁止）

## 4. リンク集
- `specs/README.md`
- `docs/architecture.md`
- `codex_workspace_standard/templates/design_docs_roles.md`

## 運用Tips
- SteeringファイルはPRレビューの一部として更新する。
- Codexに大きな依頼をする前に、関連するSteeringファイルのパスを明示すると回答精度が上がります。
