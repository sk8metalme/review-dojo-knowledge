# Readability - Markdown

## Markdownドキュメントでコードブロックに言語指定を追加

- **重要度**: info
- **発生回数**: 1
- **概要**: フェンスコードブロック（```）に言語指定がないとシンタックスハイライトが適用されず、可読性が低下する。markdownlint MD040ルール違反。
- **推奨対応**: すべてのコードブロックに適切な言語識別子（bash, json, text, plaintext等）を指定する。
- **コード例**:
  ```
  // NG
  ```
npm run lint
npm run test
```
  ```
  ```
  // OK
  ```bash
npm run lint
npm run test
```
  ```
- **対象ファイル例**: `CLAUDE.md`
- **参照PR**:
  - https://github.com/sk8metalme/nodejs-study/pull/8

---
## Markdownで強調の代わりに見出し構造を使用

- **重要度**: info
- **発生回数**: 1
- **概要**: 太字強調（**text**）を見出しの代わりに使用すると、文書構造が不明確になり、アクセシビリティツールが正しく解釈できない。markdownlint MD036ルール違反。
- **推奨対応**: セクションタイトルには強調ではなく適切な見出しレベル（###等）を使用する。
- **コード例**:
  ```
  // NG
  **注意: 手動公開は非推奨（CI経由を推奨）**
  ```
  ```
  // OK
  ### 注意

手動公開は非推奨です。CI経由の公開を推奨します。
  ```
- **対象ファイル例**: `CLAUDE.md`
- **参照PR**:
  - https://github.com/sk8metalme/nodejs-study/pull/8

---
