# Other - Bash

## statコマンドのプラットフォーム互換性問題

- **重要度**: info
- **発生回数**: 2
- **概要**: statコマンドの出力形式がmacOS（BSD）とLinux（GNU）で異なるため、パーミッション確認ロジックが正確に機能しない。macOSは"40700"（ファイルタイプ含む）、Linuxは"700"（パーミッションのみ）を返す
- **推奨対応**: stat出力の最後の3桁のみを抽出して比較することで、プラットフォーム間の互換性を確保する
- **対象ファイル例**: `install-global.sh`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/38

---
## sedコマンドでGNU拡張を使用すると移植性の問題が発生する

- **重要度**: warning
- **発生回数**: 1
- **概要**: sed コマンドで `\+` は GNU sed 拡張で、BSD sed（macOS デフォルト）では動作しません。また、既に `->>` となっているケースを `->>>` に変更してしまう誤マッチの可能性があります
- **推奨対応**: BSD sed（macOS）との互換性を確保するため、POSIX 互換の正規表現を使用してください。`[A-Za-z]\+` の代わりに `[A-Za-z][A-Za-z]*` を使用し、右辺のマッチで既に `>>` が含まれている場合を除外する（例：`[^>]` を使用）
- **コード例**:
  ```
  // NG
  sed -i 's/\([A-Za-z]\+\)->\([A-Za-z]\+\):/\1->>\2:/g' "$FILE"
  ```
  ```
  // OK
  # "->" → "->>"（同期呼び出し）
# 既に ">>" が含まれている場合は除外
sed -i 's/\([A-Za-z][A-Za-z]*\)->\([^>]\)/\1->>\2/g' "$FILE"
  ```
- **対象ファイル例**: `plugins/development-toolkit/agents/mermaid-validator/AGENT.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/170

---
## sedコマンドでGNU拡張と制限的なパターンを使用している

- **重要度**: warning
- **発生回数**: 1
- **概要**: ER 図リレーションシップ修正コマンドで、`\+` は GNU sed 拡張で BSD sed（macOS）では動作せず、`[A-Z_]` パターンは数字を含むエンティティ名に対応していません
- **推奨対応**: POSIX互換パターンを使用し、数字を含むエンティティ名に対応するため、`[A-Z_]+` を `[A-Z_][A-Z_0-9]*` に置き換えてください
- **コード例**:
  ```
  // NG
  sed -i 's/\([A-Z_]\+\)\s*->\s*\([A-Z_]\+\)/\1 ||--o{ \2/g' "$FILE"
  ```
  ```
  // OK
  # POSIX互換: [A-Z_]+ → [A-Z_][A-Z_0-9]* （BSD sed対応）
sed -i 's/\([A-Z_][A-Z_0-9]*\)\s*->\s*\([A-Z_][A-Z_0-9]*\)/\1 ||--o{ \2/g' "$FILE"
  ```
- **対象ファイル例**: `plugins/development-toolkit/agents/mermaid-validator/AGENT.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/170

---
