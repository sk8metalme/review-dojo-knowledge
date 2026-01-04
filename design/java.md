# Design - Java

## Java 依存関係検出の不完全な実装

- **重要度**: warning
- **発生回数**: 1
- **概要**: NullAway、ArchUnit、Spotless などの Java ツールの検出が単純な grep のみで実装されており、Maven プラグイン座標、Gradle プラグイン ID、Kotlin DSL、マルチモジュール構成に対応していない
- **推奨対応**: XML パーサー（xmllint または xq）を使用して Maven の pom.xml をパースする、または Gradle ファイルについては ripgrep の -U オプションでマルチライン検索を行う。サブモジュールも含めて再帰的に検索してください。
- **コード例**:
  ```
  // NG
  # トップレベルの pom.xml のみ検索
if ! grep -q "nullaway\|error_prone" pom.xml 2>/dev/null; then
  INFRA_MISSING+=("NullAway")
fi
  ```
  ```
  // OK
  # 再帰的に全 pom.xml を検索
if ! find . -name 'pom.xml' -exec grep -q "nullaway\|error_prone" {} \; ; then
  INFRA_MISSING+=("NullAway")
fi
# または xmllint で構造化パース
# xmllint --xpath "//groupId[text()='com.uber.nullaway']" pom.xml
  ```
- **対象ファイル例**: `plugins/michi/commands/michi/spec-impl.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
