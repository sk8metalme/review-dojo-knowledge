# Readability - Markdown

## Fenced code blocks should have language specified

- **重要度**: info
- **発生回数**: 1
- **概要**: Markdown fenced code blocks without language specification fail linter rule MD040 and may not render correctly in some viewers. This is especially important for documentation that includes ASCII diagrams or architecture visualizations.
- **推奨対応**: Always specify a language tag for fenced code blocks. For ASCII art, diagrams, or plain text content, use 'text' or 'plaintext' as the language identifier. Example: ```text instead of just ```
- **コード例**:
  ```
  // NG
  ```
┌─────────────────────────────────────────┐
│     Interfaces Layer (CLI)              │
│  - ApplyKnowledgeCli.ts                 │
└─────────────────────────────────────────┘
```
  ```
  ```
  // OK
  ```text
┌─────────────────────────────────────────┐
│     Interfaces Layer (CLI)              │
│  - ApplyKnowledgeCli.ts                 │
└─────────────────────────────────────────┘
```
  ```
- **対象ファイル例**: `README.md`
- **参照PR**:
  - $PR_URL

---
