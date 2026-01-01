# Security - Java

## SQLインジェクション対策

- **重要度**: critical
- **発生回数**: 1
- **概要**: SQLインジェクション対策が必要です
- **推奨対応**: PreparedStatementを使用してパラメータ化されたクエリを実装し、文字列結合によるSQL構築を避ける
- **コード例**:
  ```
  // NG
  String sql = "SELECT * FROM users WHERE id = " + userId;
  ```
  ```
  // OK
  PreparedStatement ps = conn.prepareStatement("SELECT * FROM users WHERE id = ?");
ps.setString(1, userId);
  ```
- **対象ファイル例**: `test.java`

---
