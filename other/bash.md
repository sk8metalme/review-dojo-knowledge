# Other - Bash

## statコマンドのプラットフォーム互換性問題

- **重要度**: info
- **発生回数**: 2
- **概要**: statコマンドの出力形式がmacOS（BSD）とLinux（GNU）で異なるため、パーミッション確認ロジックが正確に機能しない。macOSは"40700"（ファイルタイプ含む）、Linuxは"700"（パーミッションのみ）を返す
- **推奨対応**: stat出力の最後の3桁のみを抽出して比較することで、プラットフォーム間の互換性を確保する
- **対象ファイル例**: `install-global.sh`
- **参照PR**:
  - https://github.com/sk8metalme/ai-agent-setup/pull/38

---
