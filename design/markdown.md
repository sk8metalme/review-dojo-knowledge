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
- **対象ファイル例**: `plugins/development-toolkit/skills/claude-md-creator/assets/templates/library.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/60

---
## ドキュメントとコード実装の一貫性維持

- **重要度**: warning
- **発生回数**: 2
- **概要**: ドキュメント内容がPRの実装変更と矛盾している。プラグインベースのhooks.json実装（v1.8.0）を説明しているが、PRはv1.7.0へのロールバックでプラグイン側フックを削除し、グローバル配布に移行している。
- **推奨対応**: ドキュメントを削除するか、プラグインアプローチがPhase 2で試験された後にグローバル配布アプローチに置き換えられたことを明記し、現在の実装（global/hooks/guardrail-builder-hook.shとグローバル設定）を反映する。
- **対象ファイル例**: `CLAUDE-guardrail.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/61

---
## 削除された機能への推奨を更新

- **重要度**: warning
- **発生回数**: 2
- **概要**: ドキュメントで削除されたアプローチ（プラグインhooks.json）を推奨している。完全自動化にはプラグインhooks.jsonのSessionEndフックを使用すると記載されているが、このPRではプラグインフックが削除されている。
- **推奨対応**: 現在の推奨実装（グローバルSessionEndフック via install-global.sh）を反映するようドキュメントを更新する。
- **対象ファイル例**: `CLAUDE-guardrail.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/61

---
## 削除された機能のドキュメントを歴史的記録として更新

- **重要度**: warning
- **発生回数**: 2
- **概要**: プラグインhooks.jsonの構造と定義方法を説明しているが、このPRではプラグイン側のフックが削除されている。削除された機能を現在も利用可能であるかのように説明している。
- **推奨対応**: Phase 2で試験されたが削除されたことを明記（歴史的記録として）するか、グローバルフックの構造に置き換える。
- **対象ファイル例**: `CLAUDE-guardrail.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/61

---
## SessionEndとStopフックの技術仕様の正確性

- **重要度**: info
- **発生回数**: 2
- **概要**: SessionEndとStopフックの会話コンテキストに関する説明が不正確。SessionEndは「会話コンテキスト喪失」ではなく「アクセス対象外」が正確。Stopの「会話コンテキスト利用可能」は公式ドキュメントに根拠なし。
- **推奨対応**: SessionEnd=セッション終了後に実行されるため会話コンテキストへのアクセス対象外。Stop=応答終了時の停止制御用途。推奨理由を会話コンテキストではなく、実際の設計意図（SessionEnd=クリーンアップ・ロギング、Stop=停止制御）に基づいて修正する。
- **対象ファイル例**: `CLAUDE-guardrail.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/61

---
## Claude Plugin - Documentation and Configuration Consistency

- **重要度**: warning
- **発生回数**: 1
- **概要**: ドキュメント内でツールの使用方法を説明する際、設定ファイル（フロントマター）の許可設定と不整合があると実運用時にエラーになる設計上の問題
- **推奨対応**: プラグイン・スキルの設計時には、ドキュメントで説明する機能と、実際の権限設定（allowed-tools）を一致させること。説明と実装の乖離を防ぐため、レビュー時に両者の整合性を確認するチェックリストを用意することが推奨される。
- **コード例**:
  ```
  // NG
  # Documentation describes using Task tool
# But frontmatter doesn't grant permission
---
allowed-tools: Read, Write
---
Use Task tool for parallel execution...
  ```
  ```
  // OK
  # Documentation and permissions are aligned
---
allowed-tools: Read, Write, Task
---
Use Task tool for parallel execution...
  ```
- **対象ファイル例**: `plugins/design-review/skills/design-review/SKILL.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/66

---
