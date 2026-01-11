# Error-handling - Shell

## Cargo 環境ファイルの存在チェック不足

- **重要度**: warning
- **発生回数**: 1
- **概要**: ~/.cargo/env が存在しない環境で無条件にソースするとシェル起動時にエラーが発生する
- **推奨対応**: ファイルの存在チェックを行い、存在する場合のみソースする
- **対象ファイル例**: `.zshenv`

---
## エラー抑制によるトラブルシューティングの困難化

- **重要度**: warning
- **発生回数**: 1
- **概要**: 2>/dev/null でエラーメッセージを完全に隠蔽すると、デバッグが困難になる
- **推奨対応**: エラーメッセージをキャプチャして条件付きで表示するか、フォールバック処理を実装する
- **コード例**:
  ```
  // NG
  ccstatusline_output=$(echo "$input" | ccstatusline 2>/dev/null)
  ```
  ```
  // OK
  ccstatusline_output=$(echo "$input" | ccstatusline 2>&1)
if [ $? -ne 0 ]; then
  echo "Error: ccstatusline failed" >&2
  exit 1
fi
  ```
- **対象ファイル例**: `global/hooks/statusline.sh`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/50

---
