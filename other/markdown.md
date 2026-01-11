# Other - Markdown

## 外部リポジトリのコミット参照の検証

- **重要度**: critical
- **発生回数**: 1
- **概要**: ドキュメント内で外部リポジトリのコミットハッシュを参照する際、そのコミットが実際に存在することを確認する必要がある。存在しないコミットへのリンクは404エラーとなり、読者に誤った情報を提供することになる。
- **推奨対応**: 外部リポジトリへのコミット参照を記載する前に、以下を確認してください：
1) コミットハッシュが正確であること
2) リンクが有効であること（実際にアクセスして確認）
3) 無効な参照は削除するか、正しいハッシュ/公式ドキュメントのURLに置き換える
- **コード例**:
  ```
  // NG
  **参考:** [Commit 870624f](https://github.com/anthropics/claude-code/commit/870624fc1581a70590e382f263e2972b3f1e56f5) - Skills のスラッシュコマンドメニュー対応
  ```
  ```
  // OK
  **参考:** [Claude Code Skills Documentation](https://docs.anthropic.com/claude-code/skills) - Skills のスラッシュコマンドメニュー対応

# または、有効なコミットハッシュを使用
**参考:** [Commit abc1234](https://github.com/anthropics/claude-code/commit/abc1234567890abcdef) - Skills のスラッシュコマンドメニュー対応
  ```
- **対象ファイル例**: `CLAUDE.md`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/54

---
