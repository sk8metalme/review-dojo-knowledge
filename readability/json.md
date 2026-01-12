# Readability - Json

## JSON形式でのコメント使用に関する注意

- **重要度**: warning
- **発生回数**: 1
- **概要**: JSONサンプルコード内に標準JSONでは無効なインラインコメントが含まれており、ユーザーがそのまま使用するとパースエラーが発生する可能性がある
- **推奨対応**: JSONコードブロック内のコメントを削除するか、コードブロックの言語指定を `jsonc` (JSON with Comments) に変更する。または、コメントをJSON外部に説明として記載する。
- **コード例**:
  ```
  // NG
  {
  "plugins": [
    {
      "name": "my-plugin",
      "source": "./plugins/my-plugin",
      "version": "1.0.0",
      "skills": ["./skills/my-skill"]  // ← これが必須！
    }
  ]
}
  ```
  ```
  // OK
  {
  "plugins": [
    {
      "name": "my-plugin",
      "source": "./plugins/my-plugin",
      "version": "1.0.0",
      "skills": ["./skills/my-skill"]
    }
  ]
}

> **Note:** `skills` 配列の定義が必須です。
  ```
- **対象ファイル例**: `CLAUDE.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/57

---
