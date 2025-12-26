# Readability - Nodejs

## Remove unused imports to reduce bundle size

- **重要度**: info
- **発生回数**: 1
- **概要**: The imports 'unified', 'remarkParse', and 'remarkStringify' are declared but never used in the code. The parseKnowledgeFile function uses regex-based parsing instead of these libraries, making these imports dead code.
- **推奨対応**: Remove the unused imports (unified, remark-parse, remark-stringify) from the file. This will reduce bundle size and improve code clarity. After removal, run linter/TypeScript checks to ensure no other references remain.
- **コード例**:
  ```
  // NG
  import { readFile, writeFile, mkdir } from 'fs/promises';
import { existsSync } from 'fs';
import { join, dirname } from 'path';
import { unified } from 'unified';
import remarkParse from 'remark-parse';
import remarkStringify from 'remark-stringify';
  ```
  ```
  // OK
  import { readFile, writeFile, mkdir } from 'fs/promises';
import { existsSync } from 'fs';
import { join, dirname } from 'path';
  ```
- **対象ファイル例**: `scripts/apply-knowledge.js`
- **参照PR**:
  - https://github.com/sk8metalme/review-dojo/pull/11

---
