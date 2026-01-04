# Other - Nodejs

## 存在しない npm パッケージの参照

- **重要度**: critical
- **発生回数**: 1
- **概要**: ts-arch-kit という npm パッケージは存在せず、正しいパッケージ名は tsarch である
- **推奨対応**: パッケージ名を tsarch に修正してください。インストールコマンドは npm install --save-dev tsarch、Jest マッチャーのインポートは tsarch/dist/jest です。
- **コード例**:
  ```
  // NG
  # 存在しないパッケージ
npm install --save-dev ts-arch-kit
import "ts-arch-kit/jest"
  ```
  ```
  // OK
  # 正しいパッケージ名
npm install --save-dev tsarch
import "tsarch/dist/jest"
  ```
- **対象ファイル例**: `plugins/michi/commands/michi/spec-tasks.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/166

---
