# ChaTalk
　チャットでディベートができるアプリケーション

# URL
　デプロイ次第記述します

# 接続情報
　Basic認証　ID:takuya pass:1192
　テストアカウント　Email:test@gmail.com pass:test123

# 利用方法
　テストアカウントでログイン→ルームの作成・参加→コメント

# 目的
　自分の意見を言語化し相手に伝える能力を養うため

# 要件
- ユーザー管理機能
　ログインしたユーザーのみ参加できる
- チャットルーム作成機能
　自分でルームを作成できる
- 退室機能
　自分が退室したい時に退室できる

# 実装予定の要件
- ルーム人数制限機能
　入室できる人数を制限できる
- ルームパスワード管理機能
　パスワードを知っているユーザーが特定のルームに入室できる
- 時間経過確認機能
　議論時間がどのくらい経過したかわかる
- ルーム検索機能
　入室したいルームを検索できる
- チーム分け機能
　ルーム内のユーザーをチーム分けをして議論ができる
- 観戦機能
　議論には参加せずにルームに参加できる（入室制限人数のカウントとは別）

# DB設計
## users テーブル

| Column   | Type   | Options     |
| -------- | ------ | ----------- |
| name     | string | null: false |
| email    | string | null: false |
| password | string | null: false |

### Association

- has_many :room_users
- has_many :rooms, through: room_users
- has_many :messages

## rooms テーブル

| Column | Type   | Options     |
| ------ | ------ | ----------- |
| name   | string | null: false |

### Association

- has_many :room_users
- has_many :users, through: room_users
- has_many :messages

## room_users テーブル

| Column | Type       | Options                        |
| ------ | ---------- | ------------------------------ |
| user   | references | null: false, foreign_key: true |
| room   | references | null: false, foreign_key: true |

### Association

- belongs_to :room
- belongs_to :user

## messages テーブル

| Column  | Type       | Options                        |
| ------- | ---------- | ------------------------------ |
| content | string     |                                |
| user    | references | null: false, foreign_key: true |
| room    | references | null: false, foreign_key: true |

### Association

- belongs_to :room
- belongs_to :user

# 開発情報
　ruby 6.0.3.3