---
description: "Use when: implementing features on the inventory management hands-on project. Applies to code reviews, architecture decisions, testing, and documentation. Respond in Japanese, favor minimal viable solutions for learning context, prefer specification-driven design, and prioritize API/UI coherence over complexity."
---

# Copilot Inventory Hands-on Project Guidelines

本ファイルは、GitHub Copilot を使ったハンズオン学習向けの在庫管理アプリケーションの実装と Code Review に適用される指示です。

## 言語・コミュニケーション

- **日本語で応答する**。すべての説明、コード例、コメント、解説を日本語で行う。
- 専門用語は原語でもよいが、初出時に簡潔に説明する。
- Code Review コメントも日本語で記載する。

## アーキテクチャ・設計原則

### 最小構成優先

- **学習用であることを優先**。本番環境向けの過度な設計は避ける。
- データ永続化（DB 導入）、認証・権限制御、複雑な状態管理ライブラリは初期スコープに含めない。
- まず動作する最小構成を完成させてから、必要に応じて拡張。

### 仕様駆動の設計

- [SPEC.md](../../SPEC.md) を実装の基準とする。
- 受け入れ条件（期待するふるまい）に照らして実装判断を行う。
- 仕様の曖昧性は「実装時に決定してよい」と明記されていない限り、事前に SPEC へ反映させる。

### API と UI の整合性

- FastAPI バックエンド（/api に集約）と React フロントエンド（同一オリジン経由）の通信は明確に分離。
- エラーレスポンス（422、404、409）をバックエンドで決定し、フロントは期待値に沿って表示。
- 開発時の接続トラブル（Failed to fetch など）を避けるため、Vite プロキシ経由を標準とする。

## 実装スタイル

### ファイル分割と可読性

- 責務を明確に分割：backend/store.py（データ層）、backend/models.py（スキーマ）、backend/main.py（API ルート）
- フロント：services/api.ts（通信）、types/product.ts（型）、components/*.tsx（UI）
- 各ファイルは 150 〜 200 行以内を目安に、読みやすさを優先。

## Code Review でのチェック項目

Reviewing PRs for this project, ensure:

1. **仕様遵守**：SPEC.md の要件を満たしているか。 
2. **最小性**：スコープ外の機能（DB、認証など）が入っていないか。
3. **整合性**：バックエンド・フロントの通信仕様が一致しているか。エラーハンドリングが対称的か。
4. **可読性**：コードが読みやすく保守しやすいか。ファイル分割は適切か。
5. **テスト**：バックエンド単体テストが追加されているか。フロントはビルド成功と型チェック合格か。