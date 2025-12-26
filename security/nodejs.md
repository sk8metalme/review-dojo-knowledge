# Security - Nodejs

## SQL Injection Vulnerability - String Concatenation in Query

- **重要度**: critical
- **発生回数**: 1
- **概要**: The code constructs SQL queries using string concatenation, which is vulnerable to SQL injection attacks. User input is directly interpolated into the query string without sanitization.
- **推奨対応**: Use prepared statements with parameterized queries. Pass user input as separate parameters rather than concatenating them into the query string. This ensures proper escaping and prevents SQL injection.
- **対象ファイル例**: `example-user-service.js`

---
## Outdated Vitest version poses security risk

- **重要度**: warning
- **発生回数**: 1
- **概要**: vitest and @vitest/ui are significantly outdated (v1.1.0 from early 2024) while the latest stable version is v4.0.16 (Dec 2025). Using outdated testing frameworks can introduce security vulnerabilities and miss important bug fixes.
- **推奨対応**: Upgrade vitest and @vitest/ui to the latest stable version (^4.0.16). Note that this is a major version upgrade and may include breaking changes. Review the migration guide, update test configurations if needed, and run the full test suite to ensure compatibility.
- **コード例**:
  ```
  // NG
  "devDependencies": {
  "@vitest/ui": "^1.1.0",
  "vitest": "^1.1.0"
}
  ```
  ```
  // OK
  "devDependencies": {
  "@vitest/ui": "^4.0.16",
  "vitest": "^4.0.16"
}
  ```
- **対象ファイル例**: `package.json`
- **参照PR**:
  - https://github.com/sk8metalme/review-dojo/pull/11

---
## esbuild CORS vulnerability requires immediate patching

- **重要度**: critical
- **発生回数**: 1
- **概要**: GHSA-67mh-4wv8-2f99 is a CORS vulnerability in esbuild's development server (--serve) that allows external websites to read compiled code and source maps (CVSS 5.3). The vulnerability affects esbuild <= 0.24.2 and is fixed in 0.25.0. The current status incorrectly marks this as 'acknowledged' with a note about breaking changes, but 0.25.0 is a non-breaking patch release.
- **推奨対応**: Upgrade esbuild to version >=0.25.0 immediately. This is a non-breaking update that resolves the security vulnerability. Update package.json devDependencies and lockfile, then run CI/tests to verify the upgrade.
- **コード例**:
  ```
  // NG
  "SEC-006": {
  "id": "SEC-006",
  "title": "依存関係の脆弱性（esbuild）",
  "severity": "medium",
  "status": "acknowledged",
  "location": "package.json (devDependencies)",
  "cve": "GHSA-67mh-4wv8-2f99",
  "note": "devDependenciesのみ。本番環境には影響なし。破壊的変更が必要なため、将来のメジャーアップデート時に対応予定"
}
  ```
  ```
  // OK
  "SEC-006": {
  "id": "SEC-006",
  "title": "依存関係の脆弱性（esbuild）",
  "severity": "medium",
  "status": "fixed",
  "location": "package.json (devDependencies)",
  "cve": "GHSA-67mh-4wv8-2f99",
  "fix": "esbuildを0.25.0以上にアップグレード（非破壊的パッチ）"
}
  ```
- **対象ファイル例**: `security-scan/state.json`
- **参照PR**:
  - https://github.com/sk8metalme/review-dojo/pull/11

---
