# Error-handling - Shell

## Cargo 環境ファイルの存在チェック不足

- **重要度**: warning
- **発生回数**: 1
- **概要**: ~/.cargo/env が存在しない環境で無条件にソースするとシェル起動時にエラーが発生する
- **推奨対応**: ファイルの存在チェックを行い、存在する場合のみソースする
- **コード例**:
  ```
  // NG
  . "$HOME/.cargo/env"
  ```
  ```
  // OK
  # Cargo
if [ -f "$HOME/.cargo/env" ]; then
    . "$HOME/.cargo/env"
fi
  ```
- **対象ファイル例**: `.zshenv`

---
