# Design - Github-actions

## GitHub Actions: peter-evans/repository-dispatch v4 アップグレード時のランナーバージョン要件

- **重要度**: warning
- **発生回数**: 1
- **概要**: peter-evans/repository-dispatch@v4 にアップグレードする際、self-hosted ランナーを使用している場合は Actions Runner v2.327.1 以上が必須（Node 24 サポート対応）。GitHub ホストランナーの場合は影響なし。
- **推奨対応**: self-hosted ランナーを使用する場合は Actions Runner v2.327.1 以上にアップグレードすること。コア入力（token、repository、event-type、client-payload）に変更はないため、その他の互換性問題はない。
- **コード例**:
  ```
  // NG
  # v2 から v4 にアップグレード時、self-hosted ランナーのバージョンを確認していない
uses: peter-evans/repository-dispatch@v4
  ```
  ```
  // OK
  # v4 にアップグレード前に self-hosted ランナーを v2.327.1+ に更新
# または GitHub ホストランナーを使用
uses: peter-evans/repository-dispatch@v4
# runs-on: ubuntu-latest # GitHub ホストランナーの場合は問題なし
  ```
- **対象ファイル例**: `.github/workflows/trigger-knowledge-collection.yml`
- **参照PR**:
  - https://github.com/sk8metalme/review-dojo-knowledge/pull/3

---
