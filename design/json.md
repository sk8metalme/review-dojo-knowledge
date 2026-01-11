# Design - Json

## プラグインマニフェストの相対パス参照

- **重要度**: warning
- **発生回数**: 1
- **概要**: プラグインマニフェスト（plugin.json）でスキルファイルを参照する際、ディレクトリ構造に基づいた正確な相対パスを使用する必要がある。.claude-plugin/ディレクトリ内のmanifestから親ディレクトリ下のリソースを参照する場合は「../」を使用する。
- **推奨対応**: マニフェストファイルの位置を基準に、参照するスキルファイルへの相対パスを正確に記述してください。ディレクトリ構造を確認し、必要に応じて「../」で親ディレクトリを指定する。
- **コード例**:
  ```
  // NG
  "skills": [
  "./skills/dd/SKILL.md"
]
  ```
  ```
  // OK
  "skills": [
  "../skills/dd/SKILL.md"
]
  ```
- **対象ファイル例**: `plugins/dd/.claude-plugin/plugin.json`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/54

---
