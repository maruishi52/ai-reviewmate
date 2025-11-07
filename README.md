# AI-ReviewMate

楽天レビューの自動取得＆自動返信を行うAIシステムです。

## セットアップ

### 1. Firebaseプロジェクトの作成

1. [Firebase Console](https://console.firebase.google.com/)にアクセス
2. 新しいプロジェクトを作成
3. 「Firestore Database」を有効化
4. セキュリティルールを設定（開発中は以下を設定）:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /{document=**} {
         allow read, write: if true;
       }
     }
   }
   ```
   ⚠️ **注意**: 本番環境では適切なセキュリティルールを設定してください。

### 2. Firebase設定の追加

1. Firebase Consoleで「プロジェクトの設定」を開く
2. 「アプリを追加」から「ウェブ」を選択
3. 表示された設定情報をコピー
4. `firebase-config.js` ファイルを編集して、設定情報を追加:
   ```javascript
   window.firebaseConfig = {
       apiKey: "あなたのAPIキー",
       authDomain: "あなたのプロジェクトID.firebaseapp.com",
       projectId: "あなたのプロジェクトID",
       storageBucket: "あなたのプロジェクトID.appspot.com",
       messagingSenderId: "あなたのメッセージング送信者ID",
       appId: "あなたのアプリID"
   };
   ```

### 3. index.htmlの設定を更新

`index.html` 内のFirebase設定も同様に更新してください（`firebaseConfig` オブジェクト）。

## GitHub Pagesでのデプロイ

### 方法1: GitHub Actionsを使用（推奨）

1. このリポジトリをGitHubにプッシュ
2. リポジトリの「Settings」>「Pages」に移動
3. 「Source」で「GitHub Actions」を選択
4. `main` または `master` ブランチにプッシュすると自動的にデプロイされます

### 方法2: 手動でGitHub Pagesを有効化

1. リポジトリの「Settings」>「Pages」に移動
2. 「Source」で「Deploy from a branch」を選択
3. ブランチを `main` または `master`、フォルダを `/ (root)` に設定
4. 「Save」をクリック

## ローカルでの実行

```bash
npm install
npm start
```

ブラウザで `http://localhost:8080` にアクセスしてください。

## 機能

- レビューデータをFirebase Firestoreに保存
- 保存されたデータの一覧表示
- リアルタイムでのデータ更新

## 注意事項

- Firebase設定情報は公開リポジトリに含めないことを推奨します（環境変数を使用することを検討してください）
- 本番環境では適切なFirebase Security Rulesを設定してください
