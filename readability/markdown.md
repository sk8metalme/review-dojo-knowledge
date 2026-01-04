# Readability - Markdown

## Markdownドキュメントでコードブロックに言語指定を追加

- **重要度**: info
- **発生回数**: 7
- **概要**: フェンスコードブロック（```）に言語指定がないとシンタックスハイライトが適用されず、可読性が低下する。markdownlint MD040ルール違反。
- **推奨対応**: すべてのコードブロックに適切な言語識別子（bash, json, text, plaintext等）を指定する。
- **対象ファイル例**: `CLAUDE.md`
- **参照PR**:
  - https://github.com/sk8metalme/nodejs-study/pull/8

---
## Markdownで強調の代わりに見出し構造を使用

- **重要度**: info
- **発生回数**: 7
- **概要**: 太字強調（**text**）を見出しの代わりに使用すると、文書構造が不明確になり、アクセシビリティツールが正しく解釈できない。markdownlint MD036ルール違反。
- **推奨対応**: セクションタイトルには強調ではなく適切な見出しレベル（###等）を使用する。
- **対象ファイル例**: `CLAUDE.md`
- **参照PR**:
  - https://github.com/sk8metalme/nodejs-study/pull/8

---
## マークダウン：強調記号の代わりにヘッディングを使用

- **重要度**: info
- **発生回数**: 6
- **概要**: ドキュメント構造を改善するため、強調記号 (**...**) の代わりにマークダウンヘッディング (###) を使用する
- **推奨対応**: セクションタイトルには強調記号ではなく適切なレベルのマークダウンヘッディングを使用し、目次生成やアウトライン表示を可能にする
- **対象ファイル例**: `.claude/CLAUDE.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/1

---
## Markdownリンクフラグメントは見出しと一致させる

- **重要度**: info
- **発生回数**: 5
- **概要**: README内の内部リンクのフラグメント識別子が実際の見出しと一致していなかった。markdownlint MD051ルール違反。
- **推奨対応**: 内部リンクのフラグメントは、実際の見出しのslugと完全に一致させる必要があります。見出しに番号プレフィックス（例: '1.'）がある場合、フラグメントにも含める必要があります
- **対象ファイル例**: `README.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/35

---
## ドキュメントリンクの検証を必須化

- **重要度**: critical
- **発生回数**: 1
- **概要**: マイグレーション後のドキュメント内で、存在しないファイルへのリンクが複数発見された。.michi/steering/構造への参照が壊れており、ユーザーがドキュメントを参照できない状態となっている。
- **推奨対応**: PRレビュー時にドキュメントリンクの自動検証を実装する。マイグレーションやリネーム作業後は、必ずリンク切れチェックを実行すること。CI/CDパイプラインにマークダウンリンク検証ツールを組み込むことを推奨。
- **コード例**:
  ```
  // NG
  # マイグレーション後の参照
- [構造ガイド](.michi/steering/structure.md)
- [ワークフロー](.michi/steering/workflow.md)

// 実際のファイル位置が変更されているがリンクは更新されていない
  ```
  ```
  // OK
  # マイグレーション後の検証付き参照
- [ワークフロー](./docs/guides/workflow.md)

# CI/CDでの検証例
# .github/workflows/docs-check.yml
- name: Check markdown links
  run: |
    npm install -g markdown-link-check
    find . -name '*.md' -exec markdown-link-check {} \;
  ```
- **対象ファイル例**: `docs/MIGRATION.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
## マイグレーション後の用語統一

- **重要度**: warning
- **発生回数**: 1
- **概要**: Kiroからmichiへのマイグレーション後、ドキュメント内のラベルやコマンド参照が古い名称のまま残っている。特にユーザー向けメッセージやエラー文で不整合が発生している。
- **推奨対応**: マイグレーション作業では、コードだけでなくドキュメント、エラーメッセージ、ログ出力も含めた全体的な用語の置換を実施すること。検索・置換の自動化スクリプトを用意し、手動での見落としを防ぐ。
- **コード例**:
  ```
  // NG
  # ドキュメント内のラベル
Kiro directory: {{SPEC_DIR}}  # 値は.michiを指しているのにラベルはKiro

# エラーメッセージ
console.log('先に/kiro:spec-requirements を実行してください');  # 新しいコマンドは/michi:*
  ```
  ```
  // OK
  # 統一された用語
Spec directory: {{SPEC_DIR}}  # またはMichi directory

# 更新されたエラーメッセージ
console.log('先に/michi:spec-requirements を実行してください');

# マイグレーションスクリプト例
#!/bin/bash
find . -type f \( -name '*.md' -o -name '*.ts' \) -exec sed -i 's|/kiro:|/michi:|g' {} \;
find . -type f -name '*.md' -exec sed -i 's|Kiro directory|Spec directory|g' {} \;
  ```
- **対象ファイル例**: `plugins/michi/commands/michi/confluence-sync.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
## .michiディレクトリの不在によるリンク切れ

- **重要度**: critical
- **発生回数**: 1
- **概要**: scripts/README.mdで.michiディレクトリ配下のファイルを参照しているが、リポジトリに.michiディレクトリそのものが存在しない。全てのリンクが404となっている。
- **推奨対応**: ドキュメント構造とファイルシステム構造を一致させること。存在しないディレクトリへの参照は絶対に避ける。新規ディレクトリや構造変更を伴う場合は、ファイル作成とドキュメント更新を同一PRで実施すべき。
- **コード例**:
  ```
  // NG
  # 存在しないディレクトリへの参照
- [設計ドキュメント](../.michi/specs/onion-architecture/design.md)
- [構造ガイド](../.michi/steering/structure.md)
- [ワークフローガイド](../.michi/steering/workflow.md)

// .michiディレクトリが存在しないため全てリンク切れ
  ```
  ```
  // OK
  # アプローチ1: ディレクトリとファイルを作成
mkdir -p .michi/specs/onion-architecture
mkdir -p .michi/steering
# 必要なドキュメントを配置

# アプローチ2: 既存ドキュメントへ修正
- [設計ドキュメント](./docs/architecture.md)
- [ワークフローガイド](./docs/guides/workflow.md)

# PRレビューでのチェック項目
# - 新規リンクの追加時は対象ファイルの存在確認
# - CI/CDでリンク検証を自動実行
  ```
- **対象ファイル例**: `scripts/README.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
