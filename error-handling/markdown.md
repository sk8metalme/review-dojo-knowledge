# Error-handling - Markdown

## Claude Plugin Skill Definition - Tool Permission Configuration Mismatch

- **重要度**: warning
- **発生回数**: 2
- **概要**: SKILL.md で Task ツールの使用を説明しているが、フロントマターの allowed-tools リストに Task が含まれていないため、実行時にブロックされる問題
- **推奨対応**: SKILL.md のフロントマター allowed-tools に、本文で使用を説明しているすべてのツール（Task など）を含める必要がある。ツール使用と許可設定の整合性を保つこと。
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/66

---
## ステップ

- **重要度**: info
- **発生回数**: 1
- **概要**: 
- **推奨対応**: 

---
## ステップ

- **重要度**: info
- **発生回数**: 1
- **概要**: 
- **推奨対応**: 
- **対象ファイル例**: `plugins/deep-dive/skills/deep-dive/SKILL.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/66

---
