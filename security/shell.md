# Security - Shell

## AppleScript内のシェル変数エスケープ不足

- **重要度**: warning
- **発生回数**: 1
- **概要**: AppleScriptのdo scriptブロック内でシェル変数（PROJECT_ROOT、SESSION_ID、LOG_FILE）を直接埋め込むと、空白やクォート文字が含まれる場合にスクリプトが壊れる可能性がある
- **推奨対応**: printf '%q'を使用して変数をエスケープするか、AppleScriptに環境変数経由で安全に渡す。例: ESC_PROJECT_ROOT=$(printf '%q' "$PROJECT_ROOT")のようにエスケープされた変数を作成し、do scriptブロック内で使用する
- **コード例**:
  ```
  // NG
  osascript <<EOF
tell application "Terminal"
    do script "
        cd '$PROJECT_ROOT' || exit 1
    "
end tell
EOF
  ```
  ```
  // OK
  # 変数のエスケープ
ESCAPED_PROJECT_ROOT="${PROJECT_ROOT//'/'\\'}"

osascript <<EOF
tell application "Terminal"
    do script "
        cd '$ESCAPED_PROJECT_ROOT' || exit 1
    "
end tell
EOF
  ```
- **対象ファイル例**: `plugins/guardrail-builder/hooks/guardrail-builder-hook.sh`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/62

---
