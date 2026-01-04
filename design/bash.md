# Design - Bash

## grep による設定ファイル検証の脆弱性

- **重要度**: warning
- **発生回数**: 1
- **概要**: JSON、TOML、YAML など複数形式の設定ファイルを grep で検証すると、コメント内の誤検知や形式の違いによる見落としが発生する
- **推奨対応**: 言語別に適切なパーサーを使用してください：JSON は jq、TOML は tomllib/tomli、YAML は yq など。パーサーが利用できない場合のみ grep にフォールバックする設計にすることで、堅牢性が向上します。
- **コード例**:
  ```
  // NG
  # package.json の検証
if grep -q '"strict".*true' tsconfig.json; then
  echo "strict mode enabled"
fi
# スペースやコメントで誤検知/見落とし
  ```
  ```
  // OK
  # jq を使用したパース
if command -v jq >/dev/null 2>&1; then
  if jq -e '.compilerOptions.strict == true' tsconfig.json >/dev/null 2>&1; then
    echo "strict mode enabled"
  fi
else
  # フォールバック
  grep -q '"strict".*true' tsconfig.json
fi
  ```
- **対象ファイル例**: `plugins/michi/commands/michi/spec-impl.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
