# Security - Nodejs

## SQL Injection Vulnerability - String Concatenation in Query

- **重要度**: critical
- **発生回数**: 1
- **概要**: The code constructs SQL queries using string concatenation, which is vulnerable to SQL injection attacks. User input is directly interpolated into the query string without sanitization.
- **推奨対応**: Use prepared statements with parameterized queries. Pass user input as separate parameters rather than concatenating them into the query string. This ensures proper escaping and prevents SQL injection.
- **コード例**:
  ```
  // NG
  const query = `SELECT * FROM users WHERE id = ${userId}`;
  ```
  ```
  // OK
  const query = 'SELECT * FROM users WHERE id = ?';
const result = await this.db.query(query, [userId]);
  ```
- **対象ファイル例**: `example-user-service.js`
- **参照PR**:
  - $PR_URL

---
