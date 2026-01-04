# Design - Python

## Python/PHP 設定ファイルの grep ベース検証

- **重要度**: warning
- **発生回数**: 1
- **概要**: pyproject.toml や composer.json の内容を grep で検証すると、TOML のテーブル形式や JSON のフォーマットの違いにより不正確な結果になる
- **推奨対応**: Python の pyproject.toml には tomllib/tomli、PHP の composer.json には jq を使用してパースしてください。設定ファイルの存在確認のみに簡略化し、詳細検証は各言語のツールに任せる選択肢もあります。
- **コード例**:
  ```
  // NG
  # pyproject.toml を grep で検証
if ! grep -q "ruff\|black\|flake8" pyproject.toml 2>/dev/null; then
  INFRA_MISSING+=("Linter")
fi
# コメント内のテキストでも誤検知
  ```
  ```
  // OK
  # tomllib でパース
if command -v python3 >/dev/null 2>&1; then
  python3 -c '
import sys, tomllib
with open("pyproject.toml", "rb") as f:
  data = tomllib.load(f)
  if "tool" in data and ("ruff" in data["tool"] or "black" in data["tool"]):
    sys.exit(0)
sys.exit(1)'
  if [ $? -eq 0 ]; then
    echo "Linter configured"
  fi
fi
  ```
- **対象ファイル例**: `plugins/michi/commands/michi/spec-impl.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
