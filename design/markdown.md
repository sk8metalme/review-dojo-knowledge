# Design - Markdown

## Claude Code plugin.json仕様の命名規則とキー不足の修正

- **重要度**: warning
- **発生回数**: 3
- **概要**: plugin.jsonのサポートキー表が公式Claude仕様と不一致。`skills`を`commands`に修正が必要。`mcpServers`はキャメルケース表記にすべき。また`homepage`、`category`、`tags`、`strict`などのサポート済みキーが表から漏落している。
- **推奨対応**: 公式仕様に従い、以下を修正：1) `skills`→`commands`（コマンドマークダウンファイルへのパスまたはパス配列）、2) `mcp_servers`→`mcpServers`（キャメルケース）、3) 漏落キーの追加：`homepage`（ドキュメント/プロジェクトURL）、`category`/`tags`（マーケットプレイス検索フィールド）、`strict`（マニフェスト検証の強制設定フラグ）
- **対象ファイル例**: `CLAUDE.md`
- **参照PR**:
  - https://github.com/sk8metalme/dotfiles/pull/20

---
## 無効なコマンド参照を避ける

- **重要度**: warning
- **発生回数**: 2
- **概要**: ドキュメント内で存在しないコマンドを参照しており、ユーザーが実行できない指示を提供している
- **推奨対応**: ドキュメント内でコマンドを参照する際は、そのコマンドが実際に存在することを確認する。存在しない場合は、代替コマンドに置き換えるか、該当ステップを削除する。外部プラグインが必要な場合は、前提条件として明記する
- **対象ファイル例**: `plugins/michi/commands/michi/spec-requirements.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/169

---
