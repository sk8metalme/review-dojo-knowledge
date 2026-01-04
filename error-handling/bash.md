# Error-handling - Bash

## JSONパース処理の脆弱性 - grep/sedの限界

- **重要度**: warning
- **発生回数**: 1
- **概要**: grep/sedを使用したJSON解析は、エスケープされた引用符、改行を含む値、Unicodeエスケープシーケンスを正しく処理できず、パターンマッチが失敗する可能性がある
- **推奨対応**: jqを使用した堅牢なJSON解析に置き換え、jqが利用できない環境向けにフォールバックロジックを追加する
- **コード例**:
  ```
  // NG
  file_path=$(echo "$tool_input" | grep -oE '"file_path"\s*:\s*"[^"]*"' | sed 's/"file_path"\s*:\s*"\([^"]*\)"/\1/' || echo "")
  ```
  ```
  // OK
  if command -v jq &>/dev/null; then
    file_path=$(echo "$tool_input" | jq -r '.file_path // empty' 2>/dev/null || echo "")
else
    file_path=$(echo "$tool_input" | grep -oE '"file_path"\s*:\s*"[^"]*"' | sed 's/"file_path"\s*:\s*"\([^"]*\)"/\1/' || echo "")
fi
  ```
- **対象ファイル例**: `global/hooks/protect-secrets.sh`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/38

---
