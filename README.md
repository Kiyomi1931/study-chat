# README

## users テーブル

| Column          | Type    | Options     |
| --------------- | ------- | ----------- |
| name            | string  | null: false |
| nickname        | string  | null: false |
| school_grade_id | integer | null: false |
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