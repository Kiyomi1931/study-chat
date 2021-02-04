# README
##アプリケーション名:
study-chat

##アプリケーション概要:
生徒・先生同士のチャットとオンラインでの問題演習

##URL：
デプロイ未。デプロイ後、記載いたします。

##テスト用アカウント：
ログイン機能実装後、記載いたします。

##利用方法：

##目指した課題解決：
生徒と教師がオンラインでの問題演習と理解度を共有できるようにしたい。

##洗い出した要件：
①トップページ
・サインイン・ログインボタンへ遷移できるボタンがある。
・ログイン時は、ログアウトできるボタンがある。
・チャットルームを作成できるページへアクセスできるボタンがある。
・問題演習機能へアクセスできるボタンがある。
（生徒）
・問題演習の結果得意分野や得意な能力が表示される。
・これまで解いた問題数と正答率が教科や単元ごとに表示される。
・先生からのコメントが表示される。
（先生）
・全生徒の問題演習結果と得意・不得意が表示される。
・生徒へのコメントを作成できる。

②サインイン・ログインページ
新規登録
・名前とニックネーム、e-mail、パスワードを設定する。
・生徒の場合は学年と出席番号も入力する。
・先生の場合は認証用パスワードを入力する。
・新規登録後、個人用トップページへ戻る。

ログインページ
・e-mailとパスワードを入力すると個人用トップページへアクセスできる。

③ドリル作成機能
・先生のみアクセスできる。
・学年、教科、単元、測る力（思考力・知識・表現力）・問題・模範回答を保存できる。

④問題演習機能
・学年や単元を選択し、問題演習ができる。
・解いた問題への生徒の回答と問題のジャンルを保存できる。
・回答保存後、正解・不正解がわかり、問題の解説が表示できる。
・トップページに戻るか問題演習ページへ戻るか選択できる。

⑤チャット機能
・登録ユーザーとチャットを行うルームを作成できる。
・メッセージと画像でチャットを行うことができる。
・チャットルームを削除することができる。
・チャットを書いたユーザーはチャットのメッセージや画像を編集することができる。
・チャットを書いたユーザーはチャットのメッセージや画像を削除することができる。

##実装した機能についてのGIFと説明：

##実装予定の機能

##データベース設計：
https://gyazo.com/4889a91ccb0c976e26c64edfbb63aa35

##ローカルでの動作方法

## users テーブル

| Column          | Type    | Options     |
| --------------- | ------- | ----------- |
| name            | string  | null: false |
| nickname        | string  | null: false |
| school_grade_id | integer |             |
| student_number  | integer |             |
| email           | string  | null: false |
| password        | string  | null: false |

### Association

- has_many :room_users
- has_many :rooms, through: room_users
- has_many :messages
- has_many :study_results

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

## studies テーブル

| Column       | Type    | Options     |
| ------------ | ------- | ----------- |
| grade_id     | integer | null: false |
| subject_id   | integer | null: false |
| unit_id      | integer | null: false |
| problem      | string  | null: false |
| explanation  | string  | null: false |
| model_answer | string  | null: false |

### Association
- has_many :study_results

## study_results テーブル

| Column     | Type    | Options                        |
| ---------- | ------- | ------------------------------ |
| answer     | string  | null: false                    |
| user_id    | integer | null: false, foreign_key: true |
| grade_id   | integer | null: false, foreign_key: true |
| unit_id    | integer | null: false, foreign_key: true |
| ability_id | integer | null: false, foreign_key: true |
| problem_id | integer | null: false, foreign_key: true |
| result_id  | integer | null: false, foreign_key: true |


### Association
-belongs_to :study
-belongs_to :user