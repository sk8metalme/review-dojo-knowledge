# Other - Shell

## シェルエイリアスでの環境変数設定の誤り

- **重要度**: critical
- **発生回数**: 1
- **概要**: セミコロンで区切られた環境変数設定は現在のシェルにのみ適用され、後続のコマンドに引き継がれない
- **推奨対応**: 環境変数をスペース区切りで記述するか、envコマンドを使用してコマンドに渡す
- **コード例**:
  ```
  // NG
  alias yolo="ENABLE_TOOL_SEARCH=true; ENABLE_EXPERIMENTAL_MCP_CLI=false; claude --dangerously-skip-permissions"
  ```
  ```
  // OK
  alias yolo="ENABLE_TOOL_SEARCH=true ENABLE_EXPERIMENTAL_MCP_CLI=false claude --dangerously-skip-permissions"
  ```
- **対象ファイル例**: `config/zsh/alias.zsh`

---
