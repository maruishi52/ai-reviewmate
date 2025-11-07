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

### 2. Firebase設定の追加（詳しい手順）

#### ステップ1: Firebase Consoleにアクセス
1. ブラウザで [Firebase Console](https://console.firebase.google.com/) を開く
2. Googleアカウントでログイン

#### ステップ2: プロジェクトを作成（まだ作成していない場合）
1. 「プロジェクトを追加」または「Add project」をクリック
2. プロジェクト名を入力（例: "ai-reviewmate"）
3. Google Analyticsの設定は任意（スキップ可能）
4. 「プロジェクトを作成」をクリック
5. 作成完了まで待つ（1-2分）

#### ステップ3: Firestore Databaseを有効化
1. プロジェクトが作成されたら、左側のメニューから「Firestore Database」をクリック
2. 「データベースの作成」をクリック
3. 「テストモードで開始」を選択（開発用）
4. ロケーションを選択（例: "asia-northeast1 (Tokyo)"）
5. 「有効にする」をクリック

#### ステップ4: ウェブアプリを追加して設定情報を取得
1. 左側のメニューから「⚙️ プロジェクトの設定」（歯車アイコン）をクリック
2. 下にスクロールして「マイアプリ」セクションを見つける
3. 「</>」（ウェブアイコン）をクリックして「ウェブアプリを追加」
4. アプリのニックネームを入力（例: "AI-ReviewMate Web"）
5. 「このアプリのFirebase Hostingも設定します」のチェックは外してOK
6. 「アプリを登録」をクリック

#### ステップ5: 設定情報をコピー
7. 以下のような設定情報が表示されます：
   ```javascript
   const firebaseConfig = {
     apiKey: "AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
     authDomain: "your-project-id.firebaseapp.com",
     projectId: "your-project-id",
     storageBucket: "your-project-id.appspot.com",
     messagingSenderId: "123456789012",
     appId: "1:123456789012:web:abcdef1234567890"
   };
   ```
8. この情報をコピーします

#### ステップ6: firebase-config.jsファイルを編集
9. このプロジェクトの `firebase-config.js` ファイルを開く
10. コピーした設定情報を貼り付け、以下の形式に変更：
   ```javascript
   window.firebaseConfig = {
       apiKey: "AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
       authDomain: "your-project-id.firebaseapp.com",
       projectId: "your-project-id",
       storageBucket: "your-project-id.appspot.com",
       messagingSenderId: "123456789012",
       appId: "1:123456789012:web:abcdef1234567890"
   };
   ```
   （`const firebaseConfig =` を `window.firebaseConfig =` に変更）

#### ステップ7: index.htmlの設定も更新（オプション）
11. `index.html` ファイル内の `firebaseConfig` オブジェクトも同じ値に更新してください
   - `index.html` は `firebase-config.js` から自動的に設定を読み込むため、このステップは必須ではありません
   - ただし、両方に同じ設定を入れておくと安全です

📖 **より詳しい手順**: `FIREBASE_SETUP.md` ファイルも参照してください

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
