# Agent Hooks Playbook
Kiroの記事で紹介されていたフックを、Codex CLI向けに書き換えました。`.codex/hooks/*.md` を用意し、必要な場面で抜粋してCodexに投入してください。

## 1. auto-format-on-save
```
Trigger: 手動で `:w` または `Ctrl+S` 相当の保存を報告した時
Target: **/*.{cs,txt,md,json}
Instruction:
1. `rg --files` でカレントファイルを確認し、ESLint/Stylelint等があれば `npm run lint -- --fix`。
2. `prettier --write <file>` もしくは `.editorconfig` に合わせて整形。
3. 未使用import/using指示を削除。C#の場合は `dotnet format`. 調達不可なら差分提案のみ。
4. `console.log` や `System.Diagnostics.Debug.WriteLine` が残っていたら TODOコメント付きで報告。
```

## 2. react-component-scaffold（UI/HMIでも応用可）
```
Trigger: 新しいUI/画面ファイルを作るよう依頼したとき
Instruction:
1. コンポーネント本体 + CSS/スタイル + テスト + Storyを同時生成。
2. indexファイルに再エクスポートを追加。
3. 共通ラベル/シグナル名は `docs/labels.md` を参照して統一。
```

## 3. security-scanner
```
Trigger: PRレビュー前 or `git diff` が発生したとき
Instruction:
- `rg -n "(AKIA|AIza|ssh-rsa|BEGIN RSA)"` で秘密情報を検出。
- 見つけたら `.env` への移動と `.gitignore` 確認を提案。
```

## 4. i18n-sync
```
Trigger: `locales/ja/*.json` を編集したとき
Instruction:
1. `diff` で新旧キーを抽出。
2. 他言語ファイルに`TODO_TRANSLATION`や`REVIEW_REQUIRED`タグを自動追記。
3. 進捗を `docs/translation-status.md` に追記。
```

## 5. test-generator
```
Trigger: `src/**/*.ts` や `plc/**/*.st` を更新したとき
Instruction:
1. 変更箇所から公開関数/FBを検出。
2. 対応するテストファイルを探し、無ければ生成。
3. 正常/異常/境界テストを提案し、`npm run test` or `pytest` の結果を共有。
```

> ✨ ポイント: フックは「単一責任」「対象ファイルの明確化」「成功/失敗の報告方法」まで書くとCodexが迷いません。
