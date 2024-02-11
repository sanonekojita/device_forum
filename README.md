# テーブル設計

## users テーブル ###################################################################################################################

| Column             | Type   | Options                   |
| ------------------ | ------ | ------------------------- |
| nickname           | string | null: false               |
| email              | string | null: false, unique: true |
| encrypted_password | string | null: false               |

### Association
- has_many :comments
- has_many :active_relationships, class_name: "Relationship", foreign_key: :following_id
- has_many :followings, through: :active_relationships, source: :follower
- has_many :passive_relationships, class_name: "Relationship", foreign_key: :follower_id
- has_many :followers, through: :passive_relationships, source: :following
- has_many :likes

## devices テーブル ###################################################################################################################

| Column           | Type       | Options                        |
| ---------------- | ---------- | ------------------------------ |
| device_type_id   | references | null: false, foreign_key: true |

### Association
- has_many :comments
- has_many :likes
- has_one :mouse_device
- has_one :mouse_pad


## mouse_devices テーブル ###################################################################################################################

| Column                        | Type       | Options                        |
| ----------------------------- | ---------- | ------------------------------ |
| device_id                     | references | null: false, foreign_key: true |
| mouse_name                    | string     | null: false                    |
| mouse_mouse_shape_id          | references | null: false, foreign_key: true |
| how_to_connect_mouse_id       | references | null: false, foreign_key: true |
| mouse_length                  | integer    | null: false                    |
| mouse_width                   | integer    | null: false                    |
| mouse_height                  | integer    | null: false                    |
| mouse_battery_life            | integer    | null: false                    |
| mouse_switch_id               | references | null: false, foreign_key: true |
| mouse_sensor_id               | references | null: false, foreign_key: true |
| mouse_maximum_polling_rate_id | references | null: false, foreign_key: true |
| number_of_mouse_buttons       | integer    | null: false                    |

### Association
- belongs_to :device


## mouse_pads テーブル ###################################################################################################################

| Column              | Type       | Options                        |
| ------------------- | ---------- | ------------------------------ |
| device_id           | references | null: false, foreign_key: true |
| mouse_pad_name      | string     | null: false                    |
| mouse_pad_material  | references | null: false, foreign_key: true |
| mouse_pad_width     | integer    | null: false                    |
| mouse_pad_height    | integer    | null: false                    |
| mouse_pad_thickness | integer    |                                |

### Association
- belongs_to :device


## comments テーブル ###################################################################################################################

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| comment   | string     | null: false                    |
| user      | references | null: false, foreign_key: true |
| device_id | references | null: false, foreign_key: true |

### Association
- belongs_to :user
- belongs_to :device


## relationships テーブル ###################################################################################################################

| Column    | Type       | Options     |
| --------- | ---------- | ----------- |
| following | references | null: false |
| follower  | references | null: false |

### Association
- belongs_to :following, class_name: "User"
- belongs_to :follower, class_name: "User"


## likes テーブル ###################################################################################################################

| Column | Type       | Options                        |
| ------ | ---------- | ------------------------------ |
| user   | references | null: false, foreign_key: true |
| device | references | null: false, foreign_key: true |

### Association
- belongs_to :user
- belongs_to :device