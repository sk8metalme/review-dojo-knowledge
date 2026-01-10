# Design - Bash

## grep による設定ファイル検証の脆弱性

- **重要度**: warning
- **発生回数**: 1
- **概要**: JSON、TOML、YAML など複数形式の設定ファイルを grep で検証すると、コメント内の誤検知や形式の違いによる見落としが発生する
- **推奨対応**: 言語別に適切なパーサーを使用してください：JSON は jq、TOML は tomllib/tomli、YAML は yq など。パーサーが利用できない場合のみ grep にフォールバックする設計にすることで、堅牢性が向上します。
- **対象ファイル例**: `plugins/michi/commands/michi/spec-impl.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
## jqマージ演算子の順序に注意

- **重要度**: warning
- **発生回数**: 1
- **概要**: jqの`*`演算子を使用したマージで、引数の順序によって上書き優先順位が決まる。`.[0] * .[1]`では右辺（.[1]）が左辺（.[0]）を上書きする。
- **推奨対応**: ユーザーのカスタマイズを保持したい場合は、テンプレートを先（.[0]）、ユーザー設定を後（.[1]）に配置する。つまり`jq -s '.[0] * .[1]' "$template" "$settings"`とすることで、既存のユーザー設定が優先される。
- **コード例**:
  ```
  // NG
  jq -s '.[0] * .[1]' "$settings" "$template"
  ```
  ```
  // OK
  jq -s '.[0] * .[1]' "$template" "$settings"
  ```
- **対象ファイル例**: `install-global.sh`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/48

---
