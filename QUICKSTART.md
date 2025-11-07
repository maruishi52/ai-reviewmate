# クイックスタートガイド

## 5分でデプロイ

### 1. GitHubリポジトリを作成

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git branch -M main
git push -u origin main
```

### 2. Netlifyでデプロイ

1. https://www.netlify.com/ にアクセス
2. 「Add new site」→「Import an existing project」
3. GitHubリポジトリを選択
4. デプロイ設定（自動検出されます）
5. 「Deploy site」をクリック

### 3. Firebase設定確認

1. https://console.firebase.google.com/ にアクセス
2. プロジェクト `production-management-e9032` を選択
3. 「Realtime Database」→「ルール」タブ
4. `FIREBASE_SETUP.md`のルールをコピー＆ペースト
5. 「公開」をクリック

### 完了！

サイトがデプロイされ、Firebaseにデータが保存されます。

詳細は `DEPLOY.md` を参照してください。
