# 生産管理システム

楽天レビューの自動取得＆自動返信を行うAIシステムです。

## 機能

- 📋 **生機製織管理**: プロジェクト登録と日別製織入力
- ✅ **完了済みプロジェクト**: 完了したプロジェクトの管理
- 🏭 **生機在庫管理**: 石井加工の在庫状況と出庫管理
- 📦 **原糸在庫管理**: 原糸の入出庫登録と在庫状況
- 📅 **履歴管理**: 製織履歴と原糸入出庫履歴
- 📊 **レポート**: 統計情報と在庫サマリー

## Firebase設定

このアプリケーションはFirebase Realtime Databaseを使用してデータを保存します。

### Firebase設定情報

- **Project ID**: production-management-e9032
- **Database URL**: https://production-management-e9032-default-rtdb.asia-southeast1.firebasedatabase.app
- **Region**: asia-southeast1

### データ構造

Firebase Realtime Databaseには以下のパスでデータが保存されます：

- `/projects` - プロジェクト情報
- `/productions` - 製織実績
- `/yarns` - 原糸在庫情報
- `/ishiiStock` - 石井加工在庫
- `/ishiiShipments` - 石井加工出庫履歴

## デプロイ方法

### Netlifyでのデプロイ

1. GitHubリポジトリにプッシュ
2. Netlifyでリポジトリを接続
3. ビルドコマンド: なし（静的サイト）
4. 公開ディレクトリ: `/` (ルート)

### GitHub Pagesでのデプロイ

1. リポジトリのSettings > Pagesに移動
2. Sourceを`main`ブランチの`/ (root)`に設定
3. 自動的にデプロイされます

## ローカル開発

1. リポジトリをクローン
2. `index.html`をブラウザで開く
3. または、ローカルサーバーを起動：
   ```bash
   # Python 3の場合
   python -m http.server 8000
   
   # Node.jsの場合
   npx serve
   ```

## データ保存

- **オンラインモード**: Firebase Realtime Databaseに自動同期
- **オフラインモード**: ブラウザのlocalStorageに保存（Firebase接続時に自動同期）

## ライセンス

MIT
