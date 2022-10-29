# listing_app_bulueprint

## ER図

※矢印はポリモーフィック関連付けを表しています

![listing-app-erd](https://user-images.githubusercontent.com/87513649/198011203-86bb02df-1720-4938-857a-0b9b3899e73b.png)

## テーブル設計

### ユーザ / users

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|last_name|string|null: false||
|first_name|string|null: false||
|email|string|null: false, index: { unique: true }||
|password|string|null: false||
|crypted_password|string|null: false||
|username|string|null: false||
|public_uid|string|index: { unique: true }|gemによって作成されたランダムな文字列|
|role|integer|null: false, default: 1|{general: 1, business: 2, admin: 9}|

※Sorceryによって自動作成されるカラムは省略（activation、reset_password等）

### 組織 / organizations

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|name|string|null: false, index: { unique: true }||
|address|string|null: false||
|phone|string|null: false|integerにすると6進数化してしまう・Modelのvalidationでは「numericality: true」を付ける|
|slug|string|null: false, index: { unique: true }||


### 組織ユーザ / organization_users

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|organization_id|references|foreign_key: true|外部キー|
|user_id|references|foreign_key: true|外部キー|

※「user_id」と「organization_id」の組み合わせはユニーク


### 飲食店/ restaurants

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|name|string|null: false, index: { unique: true }||
|address|string|null: false||
|lat|float|null: false||
|lng|float|null: false||
|slug|string|null: false, index: { unique: true }||
|description|text|null: false||
|organization_id|references|foreign_key: true|外部キー|


### 飲食店カテゴリー / restaurant_categories

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|name|string|null: false, index: { unique: true }||


### 飲食店カテゴリーマッピング / restaurant_category_mappings

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|restaurant_id|references|foreign_key: true|外部キー|
|restaurant_category_id|references|foreign_key: true|外部キー|

※「restaurant_id」と「restaurant_category_id」の組み合わせはユニーク


### ショップ / shops

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|name|string|null: false, index: { unique: true }||
|address|string|null: false||
|lat|float|null: false||
|lng|float|null: false||
|slug|string|null: false, index: { unique: true }||
|description|text|null: false||
|organization_id|references|foreign_key: true|外部キー|


### ショップカテゴリー / shop_categories

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|name|string|null: false, index: { unique: true }||


### ショップカテゴリーマッピング / shop_category_mappings

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|shop_id|references|foreign_key: true|外部キー|
|shop_category_id|references|foreign_key: true|外部キー|

※「shop_id」と「shop_category_id」の組み合わせはユニーク


### 宿泊施設 / hotels

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|name|string|null: false, index: { unique: true }||
|address|string|null: false||
|lat|float|null: false||
|lng|float|null: false||
|slug|string|null: false, index: { unique: true }||
|description|text|null: false||
|organization_id|references|foreign_key: true|外部キー|


### アクティビティ / activities

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|name|string|null: false, index: { unique: true }||
|address|string|null: false||
|lat|float|null: false||
|lng|float|null: false||
|slug|string|null: false, index: { unique: true }||
|description|text|null: false||
|organization_id|references|foreign_key: true|外部キー|


### 温泉 / hot_springs

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|name|string|null: false, index: { unique: true }||
|address|string|null: false||
|lat|float|null: false||
|lng|float|null: false||
|slug|string|null: false, index: { unique: true }||
|description|text|null: false||
|organization_id|references|foreign_key: true|外部キー|


### スキー場 / ski_areas

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|name|string|null: false, index: { unique: true }||
|address|string|null: false||
|lat|float|null: false||
|lng|float|null: false||
|slug|string|null: false, index: { unique: true }||
|description|text|null: false||
|organization_id|references|foreign_key: true|外部キー|


### フォトスポット / photo_spots

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|name|string|null: false, index: { unique: true }||
|address|string|null: false||
|lat|float|null: false||
|lng|float|null: false||
|slug|string|null: false, index: { unique: true }||
|description|text|null: false||
|organization_id|references|foreign_key: true|外部キー|


### 地区マッピング / district_mappings

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|districtable_id|references|polymorphic: true|外部キー、ポリモーフィック関連|
|distlictable_type|string||ポリモーフィック関連|
|district_id|references|foreign_key: true|外部キー|

※「distictable_id」と「districtable_type」の組み合わせはユニーク


### 地区 / districts

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|name|string|null: false, index: { unique: true }||
|location|integer|null: false|{ hakuba: 1, otari: 2 }|


### 予約リンク / reservation_links

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|reservation_linkable_id|references|polymorphic: true|外部キー、ポリモーフィック関連|
|reservation_linkable_type|string||ポリモーフィック関連|
|link|string|||


### 営業時間 / opening_hours

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|opening_hourable_id|references|polymorphic: true|外部キー、ポリモーフィック関連|
|opening_hourable_type|string||ポリモーフィック関連|
|start time_hour|string|null: false||
|start time_minute|string|null: false||
|end time_hour|string|null: false||
|end time_minute|string|null: false||
|day|integer|null: false|{ monday: 1, tuesday: 2, wednesday: 3, thursday: 4, friday: 5, saturday: 6, sunday: 7, holiday: 8 }|
|closed|boolean|null: false, default: false||

※「opening_hourable_id」「opening_hourable_type」「day」の組み合わせはユニーク


### お気に入り / bookmarks

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|noticeable_id|references|polymorphic: true|外部キー、ポリモーフィック関連|
|noticeable_type|string||ポリモーフィック関連|
|user_id|references|foreign_key: true|外部キー|

※「user_id」「noticeable_id」「noticeable_type」の組み合わせはユニーク


### 投稿 / posts

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|postable_id|references|polymorphic: true|外部キー、ポリモーフィック関連|
|postable_type|string||ポリモーフィック関連|
|title|string|null: false||
|body|text|null: false||
|status|integer|null: false|{ published: 1, draft: 2 }|
|published_before|boolean|null: false| defaut: false||


### 通知/ notices

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|user_id|references|foreign_key: true|外部キー|
|noticeable_id|references|polymorphic: true|外部キー、ポリモーフィック関連|
|noticeable_type|string|null: false||
|read|boolean|null: false, default: false||


### 組織招待 / organization_invitations

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|organization_id|refenrence|foreign_key: true|外部キー|
|inviter_id|integer|null: false|※外部キーではない|
|email|string|null: false|既に同じ組織に登録されているメールアドレスはバリデーションをかけている|
|token|string|null: false, index: { unique: true }||
|expires_at|datetime|null: false||
|status|integer|null: false, default: 1|{ untouched: 1, accepted: 2, rejected: 3 }|


### 組織登録申請 / organization_registrations

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|organization_name|string|null: false|既に組織に登録されている名前は独自バリデーションで弾く|
|organization_address|string|null: false||
|organization_phone|string|null: false||
|user_id|refenrence|foreign_key: true|外部キー|
|business_detail|text|null: false||
|token|string|null: false||


### 組織登録申請アクション / organization_registration_statuses

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|organization_registration_id|references|foreign_key: true|外部キー|
|status|integer|null: false|{ accepted: 1, unaccepted: 2 }|


### ページ表示設定 / page_shows

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|page_showable_id|references|polymorphic: true|外部キー、ポリモーフィック関連|
|page_showable_type|string|null: false|ポリモーフィック関連|
|reservation_link|boolean|null: false, default: true||
|opening_hours|boolean|null: false, default: true||


### お知らせ/ announcements

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|title|string|null: false||
|body|text|null: false||
|status|integer|null: false, default: 1|{ published: 1, draft: 2, draft_to_published: 3 }|
|published_before|boolean|null: false, defaut: false||
|poster_id|integer|null: false||


### メール通知 / incoming_emails

|カラム名|データ型|オプション|メモ|
|:-|:-|:-|:-|
|user_id|references|foreign_key: true|外部キー|
|post|boolean|null: false, defaut: ture||
|annoucement|boolean|null: false, defaut: ture||
|organization|boolean|null: false, defaut: ture||
|organization_invitation|boolean|null: false, defaut: ture|

## エンドポイント

Markdownだと見にくくなってしまうため下記リンクのGoogleスプレッドシートからご確認ください

[https://docs.google.com/spreadsheets/d/1KMnVRAjFGCwj85vtm1vtErqVlCopP2kbY2h1iRZJfSE/edit#gid=776053332](https://docs.google.com/spreadsheets/d/1KMnVRAjFGCwj85vtm1vtErqVlCopP2kbY2h1iRZJfSE/edit#gid=776053332)
