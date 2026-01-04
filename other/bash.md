# Other - Bash

## statコマンドのプラットフォーム互換性問題

- **重要度**: info
- **発生回数**: 1
- **概要**: statコマンドの出力形式がmacOS（BSD）とLinux（GNU）で異なるため、パーミッション確認ロジックが正確に機能しない。macOSは"40700"（ファイルタイプ含む）、Linuxは"700"（パーミッションのみ）を返す
- **推奨対応**: stat出力の最後の3桁のみを抽出して比較することで、プラットフォーム間の互換性を確保する
- **コード例**:
  ```
  // NG
  if [[ $(stat -f "%p" "$HOME/.secrets" 2>/dev/null || stat -c "%a" "$HOME/.secrets" 2>/dev/null) != *700 ]]; then
    chmod 700 "$HOME/.secrets"
  ```
  ```
  // OK
  local current_perm=$(stat -f "%p" "$HOME/.secrets" 2>/dev/null || stat -c "%a" "$HOME/.secrets" 2>/dev/null)
if [[ "${current_perm: -3}" != "700" ]]; then
    chmod 700 "$HOME/.secrets"
    echo "✓ Fixed ~/.secrets/ permission to 700"
fi
  ```
- **対象ファイル例**: `install-global.sh`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/38

---
