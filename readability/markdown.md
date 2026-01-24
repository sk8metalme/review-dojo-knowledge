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
- **対象ファイル例**: `docs/MIGRATION.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
## マイグレーション後の用語統一

- **重要度**: warning
- **発生回数**: 1
- **概要**: Kiroからmichiへのマイグレーション後、ドキュメント内のラベルやコマンド参照が古い名称のまま残っている。特にユーザー向けメッセージやエラー文で不整合が発生している。
- **推奨対応**: マイグレーション作業では、コードだけでなくドキュメント、エラーメッセージ、ログ出力も含めた全体的な用語の置換を実施すること。検索・置換の自動化スクリプトを用意し、手動での見落としを防ぐ。
- **対象ファイル例**: `plugins/michi/commands/michi/confluence-sync.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
## .michiディレクトリの不在によるリンク切れ

- **重要度**: critical
- **発生回数**: 1
- **概要**: scripts/README.mdで.michiディレクトリ配下のファイルを参照しているが、リポジトリに.michiディレクトリそのものが存在しない。全てのリンクが404となっている。
- **推奨対応**: ドキュメント構造とファイルシステム構造を一致させること。存在しないディレクトリへの参照は絶対に避ける。新規ディレクトリや構造変更を伴う場合は、ファイル作成とドキュメント更新を同一PRで実施すべき。
- **対象ファイル例**: `scripts/README.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
## マークダウン規格: emphasis を heading に変更

- **重要度**: info
- **発生回数**: 1
- **概要**: 見出しとして機能するテキストが太字（emphasis）で表現されており、markdown の heading 記号を使用すべき
- **推奨対応**: 太字（**テキスト**）を適切な見出しレベル（#### テキスト など）に変更してください。markdownlint の MD036 ルールに準拠します。
- **対象ファイル例**: `plugins/michi/commands/michi/spec-impl.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
## マークダウン規格: コードブロックに言語指定が必要

- **重要度**: info
- **発生回数**: 1
- **概要**: フェンス付きコードブロックに言語タグが指定されていないため、markdownlint の MD040 ルールに違反している
- **推奨対応**: コードブロックの開始記号（```）の後に適切な言語タグ（bash、text、json など）を追加してください。
- **対象ファイル例**: `plugins/michi/commands/michi/spec-design.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
## Markdownのfenced code blocksに言語タグが必要

- **重要度**: info
- **発生回数**: 1
- **概要**: ディレクトリ構造を示すコードブロックに言語識別子が指定されていない
- **推奨対応**: コードブロックの開始記号を ``` から ```text に変更し、Markdownリンターが認識できるようにする
- **対象ファイル例**: `plugins/development-toolkit/skills/claude-md-creator/assets/templates/library.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/60

---
## 削除されたファイルへの参照を更新する

- **重要度**: warning
- **発生回数**: 1
- **概要**: ドキュメント内で削除済みファイルへの参照が残っており、読者を混乱させる可能性がある
- **推奨対応**: 削除されたファイルへの参照は、削除するか過去形の記述に変更する（例: 「v1.0.0 時点の実装」）
- **対象ファイル例**: `CLAUDE-guardrail.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/65

---
## Markdown Linting - Fenced Code Block Language Specifier

- **重要度**: info
- **発生回数**: 1
- **概要**: Markdown のコードブロックに言語指定がないと、MD040 lint ルールに違反し、シンタックスハイライトも適用されない
- **推奨対応**: すべてのフェンスコードブロック（```）には適切な言語指定子を追加する。プレーンテキストの場合は ```text を使用する。これにより lint エラーを回避し、可読性も向上する。
- **コード例**:
  ```
  // NG
  ```
「このプロジェクトの[対象領域]について調査してください」
```
  ```
  ```
  // OK
  ```text
「このプロジェクトの[対象領域]について調査してください」
```
  ```
- **対象ファイル例**: `plugins/deep-dive/skills/deep-dive/SKILL.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/66

---
