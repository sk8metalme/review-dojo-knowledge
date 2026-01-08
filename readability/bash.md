# Readability - Bash

## 正規表現パターンの末尾スペースによるマッチング問題

- **重要度**: info
- **発生回数**: 2
- **概要**: コマンドパターンの末尾にスペースがあることで、パイプを使用したコマンドや引数のないコマンドが正しくマッチしない
- **推奨対応**: パターン文字列から末尾スペースを削除し、単語境界（\b）または明示的な区切り文字（パイプ、セミコロン等）を使用した正規表現に変更する
- **対象ファイル例**: `global/hooks/protect-secrets.sh`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/38

---
## 正規表現パターンが引数内のカンマを含む文字列で誤検出する

- **重要度**: warning
- **発生回数**: 1
- **概要**: Rel()引数検証の正規表現パターン `Rel([^,]+,[^,]+,[^,]+,[^,]+)` は、引数内にカンマを含む文字列（例："Uses, connects"）がある場合に誤検出します
- **推奨対応**: 完全な検証には構文解析が必要ですが、より堅牢なチェックとして、開始括弧から終了括弧までを抽出し、カンマの数をカウントする方法を使用する。あるいは、この検証ステップを削除し、Mermaidパーサー自体にエラー検出を委ねることも検討してください
- **コード例**:
  ```
  // NG
  grep -E 'Rel\([^,]+,[^,]+,[^,]+,[^,]+\)' /tmp/extracted-mermaid.txt
  ```
  ```
  // OK
  # Rel()の引数チェック - 単純なカウント方式
grep -E 'Rel\(' /tmp/extracted-mermaid.txt | while read -r line; do
    # 開始括弧から終了括弧までを抽出し、引数の数を大まかにチェック
    arg_count=$(echo "$line" | grep -o ',' | wc -l)
    if [ "$arg_count" -ne 3 ]; then
        echo "WARNING: Rel() may have incorrect number of arguments: $line"
    fi
done
  ```
- **対象ファイル例**: `plugins/development-toolkit/agents/mermaid-validator/AGENT.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/170

---
## 警告メッセージが不正確で矛盾している

- **重要度**: warning
- **発生回数**: 1
- **概要**: パターンは `->` を検出していますが、警告メッセージが「Use '->' instead of '->'」となっており矛盾しています。Step 4 の修正ルールと一貫性を保つ必要があります
- **推奨対応**: 警告メッセージを "Use '->>' instead of '->'" に修正してください
- **コード例**:
  ```
  // NG
  grep -E '([A-Za-z]+)->([A-Za-z]+):' /tmp/extracted-mermaid.txt && echo "WARNING: Use '->' instead of '->'"
  ```
  ```
  // OK
  grep -E '([A-Za-z]+)->([A-Za-z]+):' /tmp/extracted-mermaid.txt && echo "WARNING: Use '->>' instead of '->'"
  ```
- **対象ファイル例**: `plugins/development-toolkit/agents/mermaid-validator/AGENT.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/170

---
