# .github/copilot-instructions.md テンプレ
> Qiita:TooMe氏の記事「GitHub Copilotを使っている人は全員"copilot-instructions.md"を作成してください」からの要点を、Codex/VS Code向けに抜粋しています。

## 1. 置き場所と読み込み順
- プロジェクト直下の `.github/copilot-instructions.md` に置くだけで、Copilot Chatが最初に読む指示書として適用される。
- VS Codeの `@workspace /new` からも作成可能だが、このテンプレを貼り付けてからプロジェクト固有情報を埋める。

## 2. 推奨セクション
1. **前提条件** — 回答言語、長大な変更時の確認フロー、SBOM/IEC62443対応、変更計画の提示など。
2. **アプリ概要** — 何を解決するアプリか、主要機能の bullet。
3. **技術スタック** — 言語/フレームワーク/主要ライブラリとバージョン。不要なimportや古い構文を避けるため必須。
4. **ディレクトリ構成** — 代表的なパスと役割（`src/features`, `plc/`, `docs/` など）。
5. **アーキテクチャ/設計指針** — MVVM, Clean Architecture, PLC FB配置など。
6. **テスト方針** — テストフレームワーク、配置（`__tests__` 等）、品質目標。
7. **アンチパターン** — 禁止事項（`default export`禁止、`any`禁止、危険なFB呼び出し等）。

## 3. 記述例（抜粋）
```md
## 前提条件
- 回答は必ず日本語。200行を超えそうな変更は計画→ユーザー確認→実装の順。
- 提案コードでは `path:line` の引用を必須とし、テストコマンドまで提示。

## 技術スタック
- 言語: TypeScript 5.x / C# 10 / iQ-R Structured Text
- フレームワーク: React 18 + Vite 5, .NET 8, GOT2000 HMI
- 状態管理: Zustand + React Query / PLC FB `SMABC`

## ディレクトリ構成
- `src/hmi/` : GOT画面とスクリプト
- `plc/` : iQ-R Structured Text、`SMABCCPU-DeviceList`
- `docs/` : プロジェクト仕様、`codex_workspace_standard`

## アンチパターン
    - `default export` は禁止、必ず名前付き。
    - `any` 型禁止。PLCの非常停止FBを直接書き換えない。
    - PoC→Pilot→実機テスト→製品初版の段階を守り、Pilot以降はIEC 62443準拠のセキュリティ設計とSBOM更新を必須化する。
```

## 4. Codexコラボのポイント
- Copilot instructions と `codex_workspace_standard/rules/*.md` に差分が出たら、両方更新して矛盾を無くす。
- 重要な制約は Copilot と Codex に同じ文言で伝える（例: 「参照先必須」「200行以上は計画提示」）。
- `.github/copilot-instructions.md` 自体も `prompts/file_search_mode.md` と同じく引用対象になるので、更新履歴を管理する。
