# Error-handling - Bash

## JSONパース処理の脆弱性 - grep/sedの限界

- **重要度**: warning
- **発生回数**: 2
- **概要**: grep/sedを使用したJSON解析は、エスケープされた引用符、改行を含む値、Unicodeエスケープシーケンスを正しく処理できず、パターンマッチが失敗する可能性がある
- **推奨対応**: jqを使用した堅牢なJSON解析に置き換え、jqが利用できない環境向けにフォールバックロジックを追加する
- **対象ファイル例**: `global/hooks/protect-secrets.sh`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/38

---
## 未初期化変数によるパラメータ展開エラー

- **重要度**: critical
- **発生回数**: 1
- **概要**: 言語が検出されない場合、配列変数(INFRA_MISSING, INFRA_OPTIONAL_MISSING, INFRA_RECOMMENDED_MISSING)とフラグ(DEVCONTAINER_MISSING)が未初期化のまま使用され、実行時エラーが発生する
- **推奨対応**: Step 2（言語検出）の直後に、全言語で共通する変数をデフォルト値で初期化してください。空配列で初期化することで、言語が未検出でも安全に処理できます。
- **コード例**:
  ```
  // NG
  # 言語検出後に初期化なし
if [ "$DETECTED_LANG" = "unknown" ]; then
  echo "言語未検出"
fi
# 後で ${#INFRA_MISSING[@]} を参照するとエラー
  ```
  ```
  // OK
  # Step 2の後に追加
INFRA_MISSING=()
INFRA_OPTIONAL_MISSING=()
INFRA_RECOMMENDED_MISSING=()
DEVCONTAINER_MISSING=false
# 各言語ブロックで必要に応じて上書き
  ```
- **対象ファイル例**: `plugins/michi/commands/michi/spec-impl.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
