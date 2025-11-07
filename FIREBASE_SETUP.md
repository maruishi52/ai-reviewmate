# Firebase設定ガイド

## Firebaseプロジェクト情報

現在のFirebase設定は`index.html`内に含まれています：

```javascript
const firebaseConfig = {
    apiKey: "AIzaSyB7ftwvUKW5-O_2E8LCE-_4rJPOSGdoaMY",
    authDomain: "production-management-e9032.firebaseapp.com",
    databaseURL: "https://production-management-e9032-default-rtdb.asia-southeast1.firebasedatabase.app",
    projectId: "production-management-e9032",
    storageBucket: "production-management-e9032.firebasestorage.app",
    messagingSenderId: "1091531720889",
    appId: "1:1091531720889:web:a66b5f83861d1a0c4bb368"
};
```

## Firebase Realtime Database セキュリティルール

Firebaseコンソールで以下のセキュリティルールを設定してください：

```json
{
  "rules": {
    "projects": {
      ".read": true,
      ".write": true
    },
    "productions": {
      ".read": true,
      ".write": true
    },
    "yarns": {
      ".read": true,
      ".write": true
    },
    "ishiiStock": {
      ".read": true,
      ".write": true
    },
    "ishiiShipments": {
      ".read": true,
      ".write": true
    }
  }
}
```

**注意**: 上記のルールは開発用です。本番環境では適切な認証とセキュリティルールを設定してください。

## セキュリティルールの設定手順

1. [Firebase Console](https://console.firebase.google.com/)にアクセス
2. プロジェクト `production-management-e9032` を選択
3. 左メニューから「Realtime Database」を選択
4. 「ルール」タブをクリック
5. 上記のルールをコピー＆ペースト
6. 「公開」をクリック

## データ構造

### projects
```
projects/
  {projectId}/
    id: string
    name: string
    productCode: string
    plannedRolls: number
    plannedMeters: number
    startDate: string
    completed: boolean
    createdDate: string
    completedDate?: string
```

### productions
```
productions/
  {productionId}/
    id: string
    projectId: string
    projectName: string
    productCode: string
    date: string
    rolls: number
    meters: number
    destination: string
    createdDate: string
```

### yarns
```
yarns/
  {yarnId}/
    id: string
    projectId?: string
    projectName?: string
    code: string
    warehouse: string
    type: "入庫" | "出庫"
    weight: number
    unit: "kg" | "ポンド"
    date: string
    note?: string
    createdDate: string
```

### ishiiStock
```
ishiiStock/
  {productCode}/
    rolls: number
    meters: number
```

### ishiiShipments
```
ishiiShipments/
  {shipmentId}/
    id: string
    productCode: string
    orderNo: string
    rolls: number
    meters: number
    date: string
    note?: string
    createdDate: string
```

## トラブルシューティング

### Firebase接続エラー

1. ブラウザのコンソールでエラーを確認
2. FirebaseプロジェクトのAPIキーが正しいか確認
3. Firebase Realtime Databaseが有効になっているか確認
4. セキュリティルールが正しく設定されているか確認

### データが保存されない

1. ネットワーク接続を確認
2. Firebaseコンソールでデータベースを確認
3. ブラウザのlocalStorageを確認（オフラインモードの場合）
