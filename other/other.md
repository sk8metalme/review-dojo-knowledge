# Other - Other

## Documentation status inconsistency between implementation and scan results

- **重要度**: info
- **発生回数**: 1
- **概要**: The summary table in security-scan/plan.md shows all 10 vulnerabilities as 'unfixed', but the PR description and code implementation (scripts/apply-knowledge.js) indicate that fixes for SEC-001 through SEC-010 have been completed. This creates confusion about the actual status of security issues.
- **推奨対応**: Update the documentation to either mark the entries as '修正済み' (fixed) or add a clear note that this file represents 'pre-fix scan results' to avoid misleading status information. Ensure table totals and counts reflect the chosen approach.
- **コード例**:
  ```
  // NG
  | カテゴリ | Critical | High | Medium | Low | Total |
|----------|----------|------|--------|-----|
| 脆弱性 | 1 | 2 | 5 | 2 | 10 |
| **修正済み** | 0 | 0 | 0 | 0 | **0** |
| **残り** | 1 | 2 | 5 | 2 | **10** |
  ```
  ```
  // OK
  # セキュリティスキャンレポート（修正前）

| カテゴリ | Critical | High | Medium | Low | Total |
|----------|----------|------|--------|-----|
| 脆弱性 | 1 | 2 | 5 | 2 | 10 |
| **修正済み** | 1 | 2 | 5 | 2 | **10** |
| **残り** | 0 | 0 | 0 | 0 | **0** |
  ```
- **対象ファイル例**: `security-scan/plan.md`
- **参照PR**:
  - https://github.com/sk8metalme/review-dojo/pull/11

---
## Replace placeholder URLs in documentation with actual references

- **重要度**: info
- **発生回数**: 1
- **概要**: Documentation contains placeholder URL (https://github.com/org/repo/pull/123) instead of actual PR references. This makes it difficult to trace the origin of security issues and their resolutions.
- **推奨対応**: Replace placeholder URLs with actual PR URLs or remove them if not applicable. If this is part of a knowledge collection system, ensure links clearly point to corresponding PRs or issues, or add a note explaining why no link is provided.
- **コード例**:
  ```
  // NG
  - **参照PR**:
  - https://github.com/org/repo/pull/123
  ```
  ```
  // OK
  - **参照PR**:
  - https://github.com/sk8metalme/review-dojo/pull/11
  - https://github.com/sk8metalme/review-dojo/issues/45
  ```
- **対象ファイル例**: `security/java.md`
- **参照PR**:
  - https://github.com/sk8metalme/review-dojo/pull/11

---
