# Design - Github-actions

## GitHub Actions: peter-evans/repository-dispatch v4 アップグレード時のランナーバージョン要件

- **重要度**: warning
- **発生回数**: 7
- **概要**: peter-evans/repository-dispatch@v4 にアップグレードする際、self-hosted ランナーを使用している場合は Actions Runner v2.327.1 以上が必須（Node 24 サポート対応）。GitHub ホストランナーの場合は影響なし。
- **推奨対応**: self-hosted ランナーを使用する場合は Actions Runner v2.327.1 以上にアップグレードすること。コア入力（token、repository、event-type、client-payload）に変更はないため、その他の互換性問題はない。
- **対象ファイル例**: `.github/workflows/trigger-knowledge-collection.yml`
- **参照PR**:
  - https://github.com/sk8metalme/review-dojo-knowledge/pull/3

---
