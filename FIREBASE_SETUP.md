# Firebase設定ガイド（画像付き手順）

このガイドでは、Firebaseの設定情報を取得する方法を詳しく説明します。

## 📋 必要なもの
- Googleアカウント
- インターネット接続

## 🚀 手順

### 1. Firebase Consoleにアクセス

1. ブラウザで以下のURLを開きます：
   ```
   https://console.firebase.google.com/
   ```

2. Googleアカウントでログインします

### 2. プロジェクトを作成

1. 画面左上の「プロジェクトを追加」または「Add project」ボタンをクリック
2. プロジェクト名を入力（例: `ai-reviewmate`）
3. 「続行」をクリック
4. Google Analyticsの設定画面が表示されますが、「このプロジェクトでGoogle Analyticsを有効にする」のチェックを外して「続行」をクリック（または有効にしてもOK）
5. 「プロジェクトを作成」をクリック
6. プロジェクトの作成が完了するまで待ちます（1-2分）

### 3. Firestore Databaseを有効化

1. プロジェクトが作成されたら、左側のメニューから「Firestore Database」をクリック
   - 見つからない場合は「構築」セクションを展開してください

2. 「データベースの作成」ボタンをクリック

3. セキュリティルールの選択：
   - **開発中**: 「テストモードで開始」を選択（推奨）
   - **本番環境**: 「本番モードで開始」を選択

4. ロケーションを選択：
   - 日本からアクセスする場合は「asia-northeast1 (Tokyo)」を選択
   - または最寄りのロケーションを選択

5. 「有効にする」をクリック
6. データベースの作成が完了するまで待ちます（1-2分）

### 4. ウェブアプリを追加

1. 左側のメニューから「⚙️ プロジェクトの設定」（歯車アイコン）をクリック
   - または、プロジェクト名の横にある歯車アイコンをクリック

2. 設定ページが開いたら、下にスクロールします

3. 「マイアプリ」セクションを見つけます

4. ウェブアプリのアイコン（`</>`）をクリック
   - 複数のアイコンがある場合、`</>` のアイコンを選択

5. アプリの登録画面が表示されます：
   - **アプリのニックネーム**: 任意の名前を入力（例: `AI-ReviewMate Web`）
   - **このアプリのFirebase Hostingも設定します**: チェックを外す（GitHub Pagesを使用するため）

6. 「アプリを登録」ボタンをクリック

### 5. 設定情報をコピー

1. 以下のようなコードが表示されます：
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

2. このコード全体をコピーします（Ctrl+C または Cmd+C）

### 6. firebase-config.jsファイルを編集

1. このプロジェクトの `firebase-config.js` ファイルを開きます

2. ファイルの内容を、コピーした設定情報で置き換えます：
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
   
   **重要**: `const firebaseConfig =` を `window.firebaseConfig =` に変更してください

3. ファイルを保存します

### 7. index.htmlの設定も更新

1. `index.html` ファイルを開きます

2. ファイル内の `firebaseConfig` オブジェクト（約140行目あたり）を見つけます

3. 同じ設定情報に更新します：
   ```javascript
   const firebaseConfig = window.firebaseConfig || {
       apiKey: "AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
       authDomain: "your-project-id.firebaseapp.com",
       projectId: "your-project-id",
       storageBucket: "your-project-id.appspot.com",
       messagingSenderId: "123456789012",
       appId: "1:123456789012:web:abcdef1234567890"
   };
   ```

4. ファイルを保存します

## ✅ 確認方法

設定が正しく完了したか確認するには：

1. ブラウザで `index.html` を開きます
2. 開発者ツール（F12キー）を開きます
3. Consoleタブを確認します
4. エラーが表示されなければ設定は成功です

## 🔒 セキュリティルールの設定

Firestore Databaseのセキュリティルールを設定します：

1. Firebase Consoleで「Firestore Database」を開く
2. 「ルール」タブをクリック
3. 以下のルールを貼り付けて「公開」をクリック：

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /reviews/{reviewId} {
      allow read, write: if true;
    }
  }
}
```

⚠️ **注意**: このルールは開発用です。本番環境では認証を要求するルールに変更してください。

## ❓ よくある質問

**Q: 設定情報が見つからない**
A: プロジェクトの設定ページで、下にスクロールして「マイアプリ」セクションを確認してください。

**Q: エラーが表示される**
A: 設定情報が正しくコピーされているか、`window.firebaseConfig =` になっているか確認してください。

**Q: データが保存されない**
A: Firestore Databaseが有効になっているか、セキュリティルールが正しく設定されているか確認してください。
