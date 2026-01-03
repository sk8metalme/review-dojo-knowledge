# Design - Markdown

## Claude Code plugin.json仕様の命名規則とキー不足の修正

- **重要度**: warning
- **発生回数**: 1
- **概要**: plugin.jsonのサポートキー表が公式Claude仕様と不一致。`skills`を`commands`に修正が必要。`mcpServers`はキャメルケース表記にすべき。また`homepage`、`category`、`tags`、`strict`などのサポート済みキーが表から漏落している。
- **推奨対応**: 公式仕様に従い、以下を修正：1) `skills`→`commands`（コマンドマークダウンファイルへのパスまたはパス配列）、2) `mcp_servers`→`mcpServers`（キャメルケース）、3) 漏落キーの追加：`homepage`（ドキュメント/プロジェクトURL）、`category`/`tags`（マーケットプレイス検索フィールド）、`strict`（マニフェスト検証の強制設定フラグ）
- **コード例**:
  ```
  // NG
  | skills | スキル定義 | いいえ |
| mcp_servers | MCPサーバー設定 | いいえ |
  ```
  ```
  // OK
  | commands | コマンドマークダウンファイルへのパスまたはパス配列 | いいえ |
| mcpServers | MCPサーバー設定（キャメルケース） | いいえ |
| homepage | ドキュメント/プロジェクトURL | いいえ |
| category | マーケットプレイスカテゴリ | いいえ |
| tags | 検索タグ配列 | いいえ |
| strict | マニフェスト検証強制フラグ | いいえ |
  ```
- **対象ファイル例**: `CLAUDE.md`
- **参照PR**:
  - https://github.com/sk8metalme/dotfiles/pull/20

---
