# デプロイ手順

このドキュメントでは、生産管理システムをGitHubでデプロイし、Firebaseにデータを保存する手順を説明します。

## 前提条件

- GitHubアカウント
- Firebaseプロジェクト（既に設定済み）
- Gitがインストールされていること

## ステップ1: GitHubリポジトリの作成

1. GitHubにログイン
2. 新しいリポジトリを作成
   - リポジトリ名: `production-management-system`（任意）
   - 公開/非公開を選択
   - README、.gitignore、ライセンスは追加しない（既にファイルがあるため）

## ステップ2: ローカルリポジトリの初期化とプッシュ

```bash
# リポジトリを初期化
git init

# すべてのファイルをステージング
git add .

# 初回コミット
git commit -m "Initial commit: Production Management System"

# GitHubリポジトリをリモートとして追加（YOUR_USERNAMEとYOUR_REPO_NAMEを置き換え）
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git

# メインブランチにプッシュ
git branch -M main
git push -u origin main
```

## ステップ3: Netlifyでのデプロイ（推奨）

### 方法A: Netlify UIを使用

1. [Netlify](https://www.netlify.com/)にログイン
2. 「Add new site」→「Import an existing project」をクリック
3. GitHubを選択してリポジトリを接続
4. ビルド設定：
   - **Build command**: （空白のまま）
   - **Publish directory**: `/` または `.`
5. 「Deploy site」をクリック
6. デプロイが完了すると、自動的にURLが生成されます

### 方法B: Netlify CLIを使用

```bash
# Netlify CLIをインストール
npm install -g netlify-cli

# Netlifyにログイン
netlify login

# サイトをデプロイ
netlify deploy --prod
```

## ステップ4: GitHub Pagesでのデプロイ（オプション）

1. GitHubリポジトリの「Settings」に移動
2. 左メニューから「Pages」を選択
3. 「Source」で「GitHub Actions」を選択
4. `.github/workflows/deploy.yml`が自動的に実行されます
5. デプロイが完了すると、`https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/`でアクセス可能

## ステップ5: Firebase設定の確認

1. [Firebase Console](https://console.firebase.google.com/)にアクセス
2. プロジェクト `production-management-e9032` を選択
3. 「Realtime Database」を確認
4. 「ルール」タブでセキュリティルールを設定（`FIREBASE_SETUP.md`を参照）

## ステップ6: 動作確認

1. デプロイされたサイトにアクセス
2. ブラウザの開発者ツール（F12）でコンソールを開く
3. 以下のメッセージが表示されることを確認：
   - `システム初期化開始`
   - `Firebase SDK検出` または `Firebase SDK未検出 - ローカルモードで動作`
4. データを入力して、Firebaseコンソールでデータが保存されることを確認

## トラブルシューティング

### Firebase接続エラー

- Firebase ConsoleでRealtime Databaseが有効になっているか確認
- セキュリティルールが正しく設定されているか確認
- ブラウザのコンソールでエラーメッセージを確認

### デプロイエラー

- `netlify.toml`の設定を確認
- GitHub Actionsのログを確認
- リポジトリのファイルが正しくプッシュされているか確認

### データが保存されない

- ネットワーク接続を確認
- Firebaseコンソールでデータベースを確認
- ブラウザのlocalStorageを確認（オフラインモードの場合）

## 継続的なデプロイ

- **Netlify**: GitHubにプッシュすると自動的にデプロイされます
- **GitHub Pages**: `main`ブランチにプッシュすると自動的にデプロイされます

## カスタムドメインの設定（オプション）

### Netlify

1. Netlifyダッシュボードでサイトを選択
2. 「Domain settings」をクリック
3. 「Add custom domain」をクリック
4. ドメイン名を入力して設定を完了

### GitHub Pages

1. リポジトリの「Settings」→「Pages」に移動
2. 「Custom domain」にドメインを入力
3. DNS設定を更新（CNAMEレコードを追加）
