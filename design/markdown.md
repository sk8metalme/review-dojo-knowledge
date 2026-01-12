# Design - Markdown

## Claude Code plugin.json仕様の命名規則とキー不足の修正

- **重要度**: warning
- **発生回数**: 4
- **概要**: plugin.jsonのサポートキー表が公式Claude仕様と不一致。`skills`を`commands`に修正が必要。`mcpServers`はキャメルケース表記にすべき。また`homepage`、`category`、`tags`、`strict`などのサポート済みキーが表から漏落している。
- **推奨対応**: 公式仕様に従い、以下を修正：1) `skills`→`commands`（コマンドマークダウンファイルへのパスまたはパス配列）、2) `mcp_servers`→`mcpServers`（キャメルケース）、3) 漏落キーの追加：`homepage`（ドキュメント/プロジェクトURL）、`category`/`tags`（マーケットプレイス検索フィールド）、`strict`（マニフェスト検証の強制設定フラグ）
- **対象ファイル例**: `CLAUDE.md`
- **参照PR**:
  - https://github.com/sk8metalme/dotfiles/pull/20

---
## 無効なコマンド参照を避ける

- **重要度**: warning
- **発生回数**: 3
- **概要**: ドキュメント内で存在しないコマンドを参照しており、ユーザーが実行できない指示を提供している
- **推奨対応**: ドキュメント内でコマンドを参照する際は、そのコマンドが実際に存在することを確認する。存在しない場合は、代替コマンドに置き換えるか、該当ステップを削除する。外部プラグインが必要な場合は、前提条件として明記する
- **対象ファイル例**: `plugins/michi/commands/michi/spec-requirements.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/169

---
## ワークフローの終了判定基準の明確化

- **重要度**: warning
- **発生回数**: 1
- **概要**: 反復的なワークフロー（質問応答サイクル等）において、終了判定基準が曖昧だと運用上の不確定性が生じる。「重要な不明点」などの抽象的な基準は具体的に定義し、最大反復回数の上限を設け、ユーザーが拒否した場合の遷移も明記する必要がある。
- **推奨対応**: 1) 終了判定で使用する用語（例：「重要な不明点」）を具体的に定義する（例：実装アーキテクチャ・要件・制約に直接影響を与える未解決事項）
- **対象ファイル例**: `plugins/dd/skills/dd/SKILL.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/54

---
## テンプレートの言語サポートと実装の不一致

- **重要度**: warning
- **発生回数**: 1
- **概要**: テンプレートが複数言語（TypeScript/Python/Go/Rust）をサポートすると主張しているが、実装例はTypeScript/npmのみである
- **推奨対応**: 以下のいずれかの対応を実施する：(1) TypeScript専用テンプレートであることを明記する、(2) 言語ごとに個別のテンプレートファイルを作成する
- **コード例**:
  ```
  // NG
  **Language**: [TypeScript/Python/Go/Rust]
**Package Manager**: [npm/PyPI/crates.io/Go modules]
  ```
  ```
  // OK
  **Language**: TypeScript
**Package Manager**: npm

# または言語別ファイルに分割:
# library.ts.md, library.py.md, library.go.md, library.rs.md
  ```
- **対象ファイル例**: `plugins/development-toolkit/skills/claude-md-creator/assets/templates/library.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/60

---
