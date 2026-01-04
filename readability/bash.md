# Readability - Bash

## 正規表現パターンの末尾スペースによるマッチング問題

- **重要度**: info
- **発生回数**: 1
- **概要**: コマンドパターンの末尾にスペースがあることで、パイプを使用したコマンドや引数のないコマンドが正しくマッチしない
- **推奨対応**: パターン文字列から末尾スペースを削除し、単語境界（\b）または明示的な区切り文字（パイプ、セミコロン等）を使用した正規表現に変更する
- **コード例**:
  ```
  // NG
  read_commands="cat |less |more |head |tail |vim |nano |vi |emacs |grep |awk |sed "
for cmd in $read_commands; do
    if echo "$bash_command" | grep -qE "^${cmd}| ${cmd}"; then
  ```
  ```
  // OK
  read_commands="cat|less|more|head|tail|vim|nano|vi|emacs|grep|awk|sed"
for cmd in ${read_commands//|/ }; do
    if echo "$bash_command" | grep -qE "(^|[|;&])\\s*${cmd}\\b"; then
  ```
- **対象ファイル例**: `global/hooks/protect-secrets.sh`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/38

---
