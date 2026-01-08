# Security - Bash

## 保護されたブランチ（main/master）への直接pushを防ぐガードが必要

- **重要度**: critical
- **発生回数**: 1
- **概要**: main/master への直接 push 禁止は重要なセキュリティルールです。実装時に、現在のブランチが main/master でないことを検証するガード条件を追加することを強く推奨します
- **推奨対応**: push実行時のフロー（Step 1 またはワークフロー開始時）に、現在のブランチを検出し、main または master の場合は処理を中止するガードを実装してください
- **コード例**:
  ```
  // NG
  # ガードなしでpushを実行
git push origin HEAD
  ```
  ```
  // OK
  # ブランチ保護チェック実装
CURRENT_BRANCH=$(git branch --show-current)
if [[ "$CURRENT_BRANCH" == "main" || "$CURRENT_BRANCH" == "master" ]]; then
    echo "❌ 保護されたブランチでは実行できません"
    exit 1
fi
# pushを実行
git push origin HEAD
  ```
- **対象ファイル例**: `plugins/development-toolkit/agents/pr-size-monitor/AGENT.md`
- **参照PR**:
  - https://github.com/sk8metalme/michi/pull/170

---
