# 実験装置予約システム — 設置手順

## ファイル構成

```
lab-reservation/
├── index.html      ← フロントエンド（予約画面）
├── api.php         ← バックエンドAPI
├── README.md       ← この手順書
└── bookings.json   ← 予約データ（自動生成されます）
```

## 設置手順

### 1. ファイルをアップロード
FTP や SFTP で、サーバーの公開ディレクトリ（例: `public_html/reservation/`）に
`index.html` と `api.php` の2ファイルをアップロードしてください。

### 2. bookings.json のパーミッション設定
初回アクセス時に `bookings.json` が自動生成されます。
もし自動生成されない場合は、空ファイルを作成してください：

```bash
echo "[]" > bookings.json
chmod 664 bookings.json
```

### 3. アクセス確認
ブラウザで `https://yourdomain.example.com/reservation/` にアクセスして
予約画面が表示されれば完了です。

## APIのパス変更について

`index.html` の先頭付近にある `API` 定数を変更することで
api.php の場所を指定できます：

```javascript
const API = 'api.php'; // デフォルト（同じディレクトリ）
```

## 装置の追加・変更

`index.html` の `EQUIPMENT` 配列を編集してください：

```javascript
const EQUIPMENT = [
  { id:'micro', name:'顕微鏡',     emoji:'🔬', color:'#2c5f8a', light:'#e8f0f8' },
  { id:'cent',  name:'遠心分離機', emoji:'⚙️', color:'#2a7a4e', light:'#e6f4ec' },
  // ここに追加...
];
```

## セキュリティについて

- 現在の実装では認証機能はありません（研究室内の信頼できるメンバー向け）
- `.htaccess` でアクセス制限を設けることを推奨します：

```apache
# .htaccess（Basic認証の例）
AuthType Basic
AuthName "Lab Reservation"
AuthUserFile /path/to/.htpasswd
Require valid-user
```

## 動作確認済み環境

- PHP 7.4 以上
- Apache / Nginx
- さくらインターネット、エックスサーバー、ロリポップ 等の共有レンタルサーバー
