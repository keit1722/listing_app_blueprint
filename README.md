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

|目的|HTTPメソッド|エンドポイント|コントローラー#アクション|
|:-|:-|:-|:-|
|トップページ表示|GET|/|pages#home|
|利用規約ページ表示|GET|/term|pages#term|
|プライバシーポリシーページ表示|GET|/privacy|pages#privacy|
|cookieポリシーページ表示|GET|/cookie|pages#cookie|
|一般ユーザ用ログインページ表示|GET|/login|sessions#new|
|一般ユーザ用ログイン処理|POST|/login|sessions#create|
|ログアウト処理|DELETE|/logout|sessions#destroy|
|ユーザ登録ページ表示|GET|/signup|users#new|
|ユーザ登録処理|POST|/signup|users#create|
|ユーザのアクティベート処理|GET|/users/:id/activate|users#activate|
|トップページで検索した結果を表示|GET|/search|pages#search|
|パスワード再設定申請処理|POST|/password_resets|password_resets#create|
|パスワード再設定申請ページ表示|GET|/password_resets/new|password_resets#new|
|パスワード再設定ページ表示|GET|/password_resets/:id/edit|password_resets#edit|
|パスワード再設定処理|PATCH/PUT|/password_resets/:id|password_resets#update|
|飲食店一覧ページから検索した結果を表示|GET|/restaurants/search|restaurants/search_forms#search|
|飲食店のお気に入り登録削除処理|DELETE|/restaurants/:restaurant_slug/bookmarks|restaurants/bookmarks#destroy|
|飲食店のお気に入り登録処理|POST|/restaurants/:restaurant_slug/bookmarks|restaurants/bookmarks#create|
|飲食店の投稿一覧ページ表示|GET|/restaurants/:restaurant_slug/posts|restaurants/posts#index|
|飲食店の投稿詳細ページ表示|GET|/restaurants/:restaurant_slug/posts/:id|restaurants/posts#show|
|飲食店一覧ページ表示|GET|/restaurants|restaurants#index|
|飲食店詳細ページ表示|GET|/restaurants/:slug|restaurants#show|
|ショップ一覧ページから検索した結果を表示|GET|/shops/search|shops/search_forms#search|
|ショップのお気に入り登録削除処理|DELETE|/shops/:shop_slug/bookmarks|shops/bookmarks#destroy|
|ショップのお気に入り登録処理|POST|/shops/:shop_slug/bookmarks|shops/bookmarks#create|
|ショップの投稿一覧ページ表示|GET|/shops/:shop_slug/posts|shops/posts#index|
|ショップの投稿詳細ページ表示|GET|/shops/:shop_slug/posts/:id|shops/posts#show|
|ショップ一覧ページ表示|GET|/shops|shops#index|
|ショップ詳細ページ表示|GET|/shops/:slug|shops#show|
|宿泊施設一覧ページから検索した結果を表示|GET|/hotels/search|hotels/search_forms#search|
|宿泊施設のお気に入り登録削除処理|DELETE|/hotels/:hotel_slug/bookmarks|hotels/bookmarks#destroy|
|宿泊施設のお気に入り登録処理|POST|/hotels/:hotel_slug/bookmarks|hotels/bookmarks#create|
|宿泊施設の投稿一覧ページ表示|GET|/hotels/:hotel_slug/posts|hotels/posts#index|
|宿泊施設の投稿詳細ページ表示|GET|/hotels/:hotel_slug/posts/:id|hotels/posts#show|
|宿泊施設一覧ページ表示|GET|/hotels|hotels#index|
|宿泊施設詳細ページ表示|GET|/hotels/:slug|hotels#show|
|アクティビティ一覧ページから検索した結果を表示|GET|/activities/search|activities/search_forms#search|
|アクティビティのお気に入り登録削除処理|DELETE|/activities/:activity_slug/bookmarks|activities/bookmarks#destroy|
|アクティビティのお気に入り登録処理|POST|/activities/:activity_slug/bookmarks|activities/bookmarks#create|
|アクティビティの投稿一覧ページ表示|GET|/activities/:activity_slug/posts|activities/posts#index|
|アクティビティの投稿詳細ページ表示|GET|/activities/:activity_slug/posts/:id|activities/posts#show|
|アクティビティ一覧ページ表示|GET|/activities|activities#index|
|アクティビティ詳細ページ表示|GET|/activities/:slug|activities#show|
|温泉一覧ページから検索した結果を表示|GET|/hot_springs/search|hot_springs/search_forms#search|
|温泉のお気に入り登録削除処理|DELETE|/hot_springs/:hot_spring_slug/bookmarks|hot_springs/bookmarks#destroy|
|温泉のお気に入り登録処理|POST|/hot_springs/:hot_spring_slug/bookmarks|hot_springs/bookmarks#create|
|温泉の投稿一覧ページ表示|GET|/hot_springs/:hot_spring_slug/posts|hot_springs/posts#index|
|温泉の投稿詳細ページ表示|GET|/hot_springs/:hot_spring_slug/posts/:id|hot_springs/posts#show|
|温泉一覧ページ表示|GET|/hot_springs|hot_springs#index|
|温泉詳細ページ表示|GET|/hot_springs/:slug|hot_springs#show|
|温泉一覧ページから検索した結果を表示|GET|/ski_areas/search|ski_areas/search_forms#search|
|温泉のお気に入り登録削除処理|DELETE|/ski_areas/:ski_area_slug/bookmarks|ski_areas/bookmarks#destroy|
|温泉のお気に入り登録処理|POST|/ski_areas/:ski_area_slug/bookmarks|ski_areas/bookmarks#create|
|温泉の投稿一覧ページ表示|GET|/ski_areas/:ski_area_slug/posts|ski_areas/posts#index|
|温泉の投稿詳細ページ表示|GET|/ski_areas/:ski_area_slug/posts/:id|ski_areas/posts#show|
|温泉一覧ページ表示|GET|/ski_areas|ski_areas#index|
|温泉詳細ページ表示|GET|/ski_areas/:slug|ski_areas#show|
|フォトスポット一覧ページから検索した結果を表示|GET|/photo_spots/search|photo_spots/search_forms#search|
|フォトスポットのお気に入り登録削除処理|DELETE|/photo_spots/:photo_spot_slug/bookmarks|photo_spots/bookmarks#destroy|
|フォトスポットのお気に入り登録処理|POST|/photo_spots/:photo_spot_slug/bookmarks|photo_spots/bookmarks#create|
|フォトスポットの投稿一覧ページ表示|GET|/photo_spots/:photo_spot_slug/posts|photo_spots/posts#index|
|フォトスポットの投稿詳細ページ表示|GET|/photo_spots/:photo_spot_slug/posts/:id|photo_spots/posts#show|
|フォトスポット一覧ページ表示|GET|/photo_spots|photo_spots#index|
|フォトスポット詳細ページ表示|GET|/photo_spots/:slug|photo_spots#show|
|通知を既読にする処理|PATCH|/notices/:id/read|notices#read|
|組織からの招待を承諾する処理|PATCH|/organization_invitations/:token/accepted|organization_invitations/actions#accepted|
|組織からの招待を拒否する処理|PATCH|/organization_invitations/:token/unaccepted|organization_invitations/actions#unaccepted|
|組織からの招待の詳細ページ表示|GET|/organization_invitations/:token|organization_invitations#show|
|お知らせ一覧ページ表示|GET|/announcements|announcements#index|
|お知らせの詳細ページ表示|GET|/announcements/:id|announcements#show|
|自分のプロフィールページを表示|GET|/mypage/profile|mypage/users#show|
|自分のプロフィールの更新処理|PATCH|/mypage/profile|mypage/users#update|
|自分のユーザアカウント削除処理|DELETE|/mypage/profile|mypage/users#destroy|
|自分のプロフィール編集ページ表示|GET|/mypage/profile/edit|mypage/users#edit|
|自分のお気に入り登録した一覧ページ表示|GET|/mypage/bookmarks|mypage/bookmarks#index|
|自分宛ての通知一覧ページ表示|GET|/mypage/notices|mypage/notices#index|
|登録申請した組織情報一覧ページ表示|GET|/mypage/organization_registrations|mypage/organization_registrations#index|
|新規組織登録申請処理|POST|/mypage/organization_registrations|mypage/organization_registrations#create|
|新規組織登録申請ページ表示|GET|/mypage/organization_registrations/new|mypage/organization_registrations#new|
|新規登録申請済み組織情報詳細ページ表示|GET|/mypage/organization_registrations/:id|mypage/organization_registrations#show|
|自分のメール受信設定詳細ページ表示|GET|/mypage/email_setting|mypage/incoming_emails#show|
|自分のメール受信設定編集ページ表示|GET|/mypage/email_setting/edit|mypage/incoming_emails#edit|
|自分のメール受信設定更新処理|PATCH|/mypage/email_setting|mypage/incoming_emails#update|
|ビジネスユーザ用ログインページ表示|GET|/business/login|business/sessions#new|
|ビジネスユーザ用ログイン処理|POST|/business/login|business/sessions#create|
|組織への招待状況一覧ページ表示|GET|/organizations/:organization_slug/organization_invitations|organizations/organization_invitations#index|
|組織への招待処理|POST|/organizations/:organization_slug/organization_invitations|organizations/organization_invitations#create|
|組織への新規招待作成ページ表示|GET|/organizations/:organization_slug/organization_invitations/new|organizations/organization_invitations#new|
|飲食店の投稿を公開状態で作成する処理|POST|/organizations/:organization_slug/restaurants/:restaurant_slug/posts/publish|organizations/restaurants/posts#publish|
|飲食店の投稿を下書き状態で作成する処理|POST|/organizations/:organization_slug/restaurants/:restaurant_slug/posts/unpublish|organizations/restaurants/posts#unpublish|
|飲食店の投稿を下書きから公開状態へ更新する処理|PATCH|/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id/to_published|organizations/restaurants/posts#to_published|
|飲食店の投稿を公開から下書き状態へ更新する処理|PATCH|/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id/to_draft|organizations/restaurants/posts#to_draft|
|飲食店の投稿を公開状態のまま更新する処理|PATCH|/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id/as_published|organizations/restaurants/posts#as_published|
|飲食店の投稿を下書き状態のまま更新する処理|PATCH|/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id/as_draft|organizations/restaurants/posts#as_draft|
|飲食店の投稿一覧ページ表示|GET|/organizations/:organization_slug/restaurants/:restaurant_slug/posts|organizations/restaurants/posts#index|
|飲食店の新規投稿作成ページ表示|GET|/organizations/:organization_slug/restaurants/:restaurant_slug/posts/new|organizations/restaurants/posts#new|
|飲食店の投稿編集ページ表示|GET|/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id/edit|organizations/restaurants/posts#edit|
|飲食店の投稿詳細ページ表示|GET|/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id|organizations/restaurants/posts#show|
|飲食店の投稿削除処理|DELETE|/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id|organizations/restaurants/posts#destroy|
|組織所属飲食店一覧ページ表示|GET|/organizations/:organization_slug/restaurants|organizations/restaurants#index|
|新規飲食店作成処理|POST|/organizations/:organization_slug/restaurants|organizations/restaurants#create|
|新規飲食店作成ページ表示|GET|/organizations/:organization_slug/restaurants/new|organizations/restaurants#new|
|飲食店情報編集ページ表示|GET|/organizations/:organization_slug/restaurants/:slug/edit|organizations/restaurants#edit|
|飲食店詳細ページ表示|GET|/organizations/:organization_slug/restaurants/:slug|organizations/restaurants#show|
|飲食店情報更新処理|PATCH/PUT|/organizations/:organization_slug/restaurants/:slug|organizations/restaurants#update|
|飲食店削除処理|DELETE|/organizations/:organization_slug/restaurants/:slug|organizations/restaurants#destroy|
|ショップの投稿を公開状態で作成する処理|POST|/organizations/:organization_slug/shops/:shop_slug/posts/publish|organizations/shops/posts#publish|
|ショップの投稿を下書き状態で作成する処理|POST|/organizations/:organization_slug/shops/:shop_slug/posts/unpublish|organizations/shops/posts#unpublish|
|ショップの投稿を下書きから公開状態へ更新する処理|PATCH|/organizations/:organization_slug/shops/:shop_slug/posts/:id/to_published|organizations/shops/posts#to_published|
|ショップの投稿を公開から下書き状態へ更新する処理|PATCH|/organizations/:organization_slug/shops/:shop_slug/posts/:id/to_draft|organizations/shops/posts#to_draft|
|ショップの投稿を公開状態のまま更新する処理|PATCH|/organizations/:organization_slug/shops/:shop_slug/posts/:id/as_published|organizations/shops/posts#as_published|
|ショップの投稿を下書き状態のまま更新する処理|PATCH|/organizations/:organization_slug/shops/:shop_slug/posts/:id/as_draft|organizations/shops/posts#as_draft|
|ショップの投稿一覧ページ表示|GET|/organizations/:organization_slug/shops/:shop_slug/posts|organizations/shops/posts#index|
|ショップの新規投稿作成ページ表示|GET|/organizations/:organization_slug/shops/:shop_slug/posts/new|organizations/shops/posts#new|
|ショップの投稿編集ページ表示|GET|/organizations/:organization_slug/shops/:shop_slug/posts/:id/edit|organizations/shops/posts#edit|
|ショップの投稿詳細ページ表示|GET|/organizations/:organization_slug/shops/:shop_slug/posts/:id|organizations/shops/posts#show|
|ショップの投稿削除処理|DELETE|/organizations/:organization_slug/shops/:shop_slug/posts/:id|organizations/shops/posts#destroy|
|組織所属ショップ一覧ページ表示|GET|/organizations/:organization_slug/shops|organizations/shops#index|
|新規ショップ作成処理|POST|/organizations/:organization_slug/shops|organizations/shops#create|
|新規ショップ作成ページ表示|GET|/organizations/:organization_slug/shops/new|organizations/shops#new|
|ショップ情報編集ページ表示|GET|/organizations/:organization_slug/shops/:slug/edit|organizations/shops#edit|
|ショップ詳細ページ表示|GET|/organizations/:organization_slug/shops/:slug|organizations/shops#show|
|ショップ情報更新処理|PATCH/PUT|/organizations/:organization_slug/shops/:slug|organizations/shops#update|
|ショップ削除処理|DELETE|/organizations/:organization_slug/shops/:slug|organizations/shops#destroy|
|宿泊施設の投稿を公開状態で作成する処理|POST|/organizations/:organization_slug/hotels/:hotel_slug/posts/publish|organizations/hotels/posts#publish|
|宿泊施設の投稿を下書き状態で作成する処理|POST|/organizations/:organization_slug/hotels/:hotel_slug/posts/unpublish|organizations/hotels/posts#unpublish|
|宿泊施設の投稿を下書きから公開状態へ更新する処理|PATCH|/organizations/:organization_slug/hotels/:hotel_slug/posts/:id/to_published|organizations/hotels/posts#to_published|
|宿泊施設の投稿を公開から下書き状態へ更新する処理|PATCH|/organizations/:organization_slug/hotels/:hotel_slug/posts/:id/to_draft|organizations/hotels/posts#to_draft|
|宿泊施設の投稿を公開状態のまま更新する処理|PATCH|/organizations/:organization_slug/hotels/:hotel_slug/posts/:id/as_published|organizations/hotels/posts#as_published|
|宿泊施設の投稿を下書き状態のまま更新する処理|PATCH|/organizations/:organization_slug/hotels/:hotel_slug/posts/:id/as_draft|organizations/hotels/posts#as_draft|
|宿泊施設の投稿一覧ページ表示|GET|/organizations/:organization_slug/hotels/:hotel_slug/posts|organizations/hotels/posts#index|
|宿泊施設の新規投稿作成ページ表示|GET|/organizations/:organization_slug/hotels/:hotel_slug/posts/new|organizations/hotels/posts#new|
|宿泊施設の投稿編集ページ表示|GET|/organizations/:organization_slug/hotels/:hotel_slug/posts/:id/edit|organizations/hotels/posts#edit|
|宿泊施設の投稿詳細ページ表示|GET|/organizations/:organization_slug/hotels/:hotel_slug/posts/:id|organizations/hotels/posts#show|
|宿泊施設の投稿削除処理|DELETE|/organizations/:organization_slug/hotels/:hotel_slug/posts/:id|organizations/hotels/posts#destroy|
|組織所属宿泊施設一覧ページ表示|GET|/organizations/:organization_slug/hotels|organizations/hotels#index|
|新規宿泊施設作成処理|POST|/organizations/:organization_slug/hotels|organizations/hotels#create|
|新規宿泊施設作成ページ表示|GET|/organizations/:organization_slug/hotels/new|organizations/hotels#new|
|宿泊施設情報編集ページ表示|GET|/organizations/:organization_slug/hotels/:slug/edit|organizations/hotels#edit|
|宿泊施設詳細ページ表示|GET|/organizations/:organization_slug/hotels/:slug|organizations/hotels#show|
|宿泊施設情報更新処理|PATCH/PUT|/organizations/:organization_slug/hotels/:slug|organizations/hotels#update|
|宿泊施設削除処理|DELETE|/organizations/:organization_slug/hotels/:slug|organizations/hotels#destroy|
|アクティビティの投稿を公開状態で作成する処理|POST|/organizations/:organization_slug/activities/:activity_slug/posts/publish|organizations/activities/posts#publish|
|アクティビティの投稿を下書き状態で作成する処理|POST|/organizations/:organization_slug/activities/:activity_slug/posts/unpublish|organizations/activities/posts#unpublish|
|アクティビティの投稿を下書きから公開状態へ更新する処理|PATCH|/organizations/:organization_slug/activities/:activity_slug/posts/:id/to_published|organizations/activities/posts#to_published|
|アクティビティの投稿を公開から下書き状態へ更新する処理|PATCH|/organizations/:organization_slug/activities/:activity_slug/posts/:id/to_draft|organizations/activities/posts#to_draft|
|アクティビティの投稿を公開状態のまま更新する処理|PATCH|/organizations/:organization_slug/activities/:activity_slug/posts/:id/as_published|organizations/activities/posts#as_published|
|アクティビティの投稿を下書き状態のまま更新する処理|PATCH|/organizations/:organization_slug/activities/:activity_slug/posts/:id/as_draft|organizations/activities/posts#as_draft|
|アクティビティの投稿一覧ページ表示|GET|/organizations/:organization_slug/activities/:activity_slug/posts|organizations/activities/posts#index|
|アクティビティの新規投稿作成ページ表示|GET|/organizations/:organization_slug/activities/:activity_slug/posts/new|organizations/activities/posts#new|
|アクティビティの投稿編集ページ表示|GET|/organizations/:organization_slug/activities/:activity_slug/posts/:id/edit|organizations/activities/posts#edit|
|アクティビティの投稿詳細ページ表示|GET|/organizations/:organization_slug/activities/:activity_slug/posts/:id|organizations/activities/posts#show|
|アクティビティの投稿削除処理|DELETE|/organizations/:organization_slug/activities/:activity_slug/posts/:id|organizations/activities/posts#destroy|
|組織所属アクティビティ一覧ページ表示|GET|/organizations/:organization_slug/activities|organizations/activities#index|
|新規アクティビティ作成処理|POST|/organizations/:organization_slug/activities|organizations/activities#create|
|新規アクティビティ作成ページ表示|GET|/organizations/:organization_slug/activities/new|organizations/activities#new|
|アクティビティ情報編集ページ表示|GET|/organizations/:organization_slug/activities/:slug/edit|organizations/activities#edit|
|アクティビティ詳細ページ表示|GET|/organizations/:organization_slug/activities/:slug|organizations/activities#show|
|アクティビティ情報更新処理|PATCH/PUT|/organizations/:organization_slug/activities/:slug|organizations/activities#update|
|アクティビティ削除処理|DELETE|/organizations/:organization_slug/activities/:slug|organizations/activities#destroy|
|温泉の投稿を公開状態で作成する処理|POST|/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/publish|organizations/hot_springs/posts#publish|
|温泉の投稿を下書き状態で作成する処理|POST|/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/unpublish|organizations/hot_springs/posts#unpublish|
|温泉の投稿を下書きから公開状態へ更新する処理|PATCH|/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id/to_published|organizations/hot_springs/posts#to_published|
|温泉の投稿を公開から下書き状態へ更新する処理|PATCH|/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id/to_draft|organizations/hot_springs/posts#to_draft|
|温泉の投稿を公開状態のまま更新する処理|PATCH|/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id/as_published|organizations/hot_springs/posts#as_published|
|温泉の投稿を下書き状態のまま更新する処理|PATCH|/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id/as_draft|organizations/hot_springs/posts#as_draft|
|温泉の投稿一覧ページ表示|GET|/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts|organizations/hot_springs/posts#index|
|温泉の新規投稿作成ページ表示|GET|/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/new|organizations/hot_springs/posts#new|
|温泉の投稿編集ページ表示|GET|/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id/edit|organizations/hot_springs/posts#edit|
|温泉の投稿詳細ページ表示|GET|/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id|organizations/hot_springs/posts#show|
|温泉の投稿削除処理|DELETE|/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id|organizations/hot_springs/posts#destroy|
|組織所属温泉一覧ページ表示|GET|/organizations/:organization_slug/hot_springs|organizations/hot_springs#index|
|新規温泉作成処理|POST|/organizations/:organization_slug/hot_springs|organizations/hot_springs#create|
|新規温泉作成ページ表示|GET|/organizations/:organization_slug/hot_springs/new|organizations/hot_springs#new|
|温泉情報編集ページ表示|GET|/organizations/:organization_slug/hot_springs/:slug/edit|organizations/hot_springs#edit|
|温泉詳細ページ表示|GET|/organizations/:organization_slug/hot_springs/:slug|organizations/hot_springs#show|
|温泉情報更新処理|PATCH/PUT|/organizations/:organization_slug/hot_springs/:slug|organizations/hot_springs#update|
|温泉削除処理|DELETE|/organizations/:organization_slug/hot_springs/:slug|organizations/hot_springs#destroy|
|スキー場の投稿を公開状態で作成する処理|POST|/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/publish|organizations/ski_areas/posts#publish|
|スキー場の投稿を下書き状態で作成する処理|POST|/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/unpublish|organizations/ski_areas/posts#unpublish|
|スキー場の投稿を下書きから公開状態へ更新する処理|PATCH|/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id/to_published|organizations/ski_areas/posts#to_published|
|スキー場の投稿を公開から下書き状態へ更新する処理|PATCH|/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id/to_draft|organizations/ski_areas/posts#to_draft|
|スキー場の投稿を公開状態のまま更新する処理|PATCH|/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id/as_published|organizations/ski_areas/posts#as_published|
|スキー場の投稿を下書き状態のまま更新する処理|PATCH|/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id/as_draft|organizations/ski_areas/posts#as_draft|
|スキー場の投稿一覧ページ表示|GET|/organizations/:organization_slug/ski_areas/:ski_area_slug/posts|organizations/ski_areas/posts#index|
|スキー場の新規投稿作成ページ表示|GET|/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/new|organizations/ski_areas/posts#new|
|スキー場の投稿編集ページ表示|GET|/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id/edit|organizations/ski_areas/posts#edit|
|スキー場の投稿詳細ページ表示|GET|/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id|organizations/ski_areas/posts#show|
|スキー場の投稿削除処理|DELETE|/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id|organizations/ski_areas/posts#destroy|
|組織所属スキー場一覧ページ表示|GET|/organizations/:organization_slug/ski_areas|organizations/ski_areas#index|
|新規スキー場作成処理|POST|/organizations/:organization_slug/ski_areas|organizations/ski_areas#create|
|新規スキー場作成ページ表示|GET|/organizations/:organization_slug/ski_areas/new|organizations/ski_areas#new|
|スキー場情報編集ページ表示|GET|/organizations/:organization_slug/ski_areas/:slug/edit|organizations/ski_areas#edit|
|スキー場詳細ページ表示|GET|/organizations/:organization_slug/ski_areas/:slug|organizations/ski_areas#show|
|スキー場情報更新処理|PATCH/PUT|/organizations/:organization_slug/ski_areas/:slug|organizations/ski_areas#update|
|スキー場削除処理|DELETE|/organizations/:organization_slug/ski_areas/:slug|organizations/ski_areas#destroy|
|フォトスポットの投稿を公開状態で作成する処理|POST|/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/publish|organizations/photo_spots/posts#publish|
|フォトスポットの投稿を下書き状態で作成する処理|POST|/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/unpublish|organizations/photo_spots/posts#unpublish|
|フォトスポットの投稿を下書きから公開状態へ更新する処理|PATCH|/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id/to_published|organizations/photo_spots/posts#to_published|
|フォトスポットの投稿を公開から下書き状態へ更新する処理|PATCH|/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id/to_draft|organizations/photo_spots/posts#to_draft|
|フォトスポットの投稿を公開状態のまま更新する処理|PATCH|/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id/as_published|organizations/photo_spots/posts#as_published|
|フォトスポットの投稿を下書き状態のまま更新する処理|PATCH|/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id/as_draft|organizations/photo_spots/posts#as_draft|
|フォトスポットの投稿一覧ページ表示|GET|/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts|organizations/photo_spots/posts#index|
|フォトスポットの新規投稿作成ページ表示|GET|/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/new|organizations/photo_spots/posts#new|
|フォトスポットの投稿編集ページ表示|GET|/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id/edit|organizations/photo_spots/posts#edit|
|フォトスポットの投稿詳細ページ表示|GET|/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id|organizations/photo_spots/posts#show|
|フォトスポットの投稿削除処理|DELETE|/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id|organizations/photo_spots/posts#destroy|
|組織所属フォトスポット一覧ページ表示|GET|/organizations/:organization_slug/photo_spots|organizations/photo_spots#index|
|新規フォトスポット作成処理|POST|/organizations/:organization_slug/photo_spots|organizations/photo_spots#create|
|新規フォトスポット作成ページ表示|GET|/organizations/:organization_slug/photo_spots/new|organizations/photo_spots#new|
|フォトスポット情報編集ページ表示|GET|/organizations/:organization_slug/photo_spots/:slug/edit|organizations/photo_spots#edit|
|フォトスポット詳細ページ表示|GET|/organizations/:organization_slug/photo_spots/:slug|organizations/photo_spots#show|
|フォトスポット情報更新処理|PATCH/PUT|/organizations/:organization_slug/photo_spots/:slug|organizations/photo_spots#update|
|フォトスポット削除処理|DELETE|/organizations/:organization_slug/photo_spots/:slug|organizations/photo_spots#destroy|
|組織一覧ページ表示|GET|/organizations|organizations#index|
|新規組織作成処理|POST|/organizations|organizations#create|
|新規組織作成ページ表示|GET|/organizations/new|organizations#new|
|組織情報編集ページ表示|GET|/organizations/:slug/edit|organizations#edit|
|組織情報詳細ページ表示|GET|/organizations/:slug|organizations#show|
|組織情報更新処理|PATCH/PUT|/organizations/:slug|organizations#update|
|組織削除処理|DELETE|/organizations/:slug|organizations#destroy|
|組織からの退会処理|DELETE|/organization_users/:slug|organization_users#destroy|
|アドミンユーザ用ログインページ表示|GET|/pvsuwimvsuoitmucvyku/login|pvsuwimvsuoitmucvyku/sessions#new|
|アドミンユーザ用ログイン処理|POST|/pvsuwimvsuoitmucvyku/login|pvsuwimvsuoitmucvyku/sessions#create|
|飲食店の投稿を下書きから公開状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id/to_published|pvsuwimvsuoitmucvyku/organizations/restaurants/posts#to_published|
|飲食店の投稿を公開から下書き状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id/to_draft|pvsuwimvsuoitmucvyku/organizations/restaurants/posts#to_draft|
|飲食店の投稿を公開状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id/as_published|pvsuwimvsuoitmucvyku/organizations/restaurants/posts#as_published|
|飲食店の投稿を下書き状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id/as_draft|pvsuwimvsuoitmucvyku/organizations/restaurants/posts#as_draft|
|飲食店の投稿一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/restaurants/:restaurant_slug/posts|pvsuwimvsuoitmucvyku/organizations/restaurants/posts#index|
|飲食店の投稿編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id/edit|pvsuwimvsuoitmucvyku/organizations/restaurants/posts#edit|
|飲食店の投稿詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/restaurants/posts#show|
|飲食店の投稿削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/restaurants/:restaurant_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/restaurants/posts#destroy|
|飲食店一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/restaurants|pvsuwimvsuoitmucvyku/organizations/restaurants#index|
|飲食店情報編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/restaurants/:slug/edit|pvsuwimvsuoitmucvyku/organizations/restaurants#edit|
|飲食店詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/restaurants/:slug|pvsuwimvsuoitmucvyku/organizations/restaurants#show|
|飲食店情報更新処理|PATCH/PUT|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/restaurants/:slug|pvsuwimvsuoitmucvyku/organizations/restaurants#update|
|飲食店削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/restaurants/:slug|pvsuwimvsuoitmucvyku/organizations/restaurants#destroy|
|ショップの投稿を下書きから公開状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/shops/:shop_slug/posts/:id/to_published|pvsuwimvsuoitmucvyku/organizations/shops/posts#to_published|
|ショップの投稿を公開から下書き状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/shops/:shop_slug/posts/:id/to_draft|pvsuwimvsuoitmucvyku/organizations/shops/posts#to_draft|
|ショップの投稿を公開状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/shops/:shop_slug/posts/:id/as_published|pvsuwimvsuoitmucvyku/organizations/shops/posts#as_published|
|ショップの投稿を下書き状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/shops/:shop_slug/posts/:id/as_draft|pvsuwimvsuoitmucvyku/organizations/shops/posts#as_draft|
|ショップの投稿一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/shops/:shop_slug/posts|pvsuwimvsuoitmucvyku/organizations/shops/posts#index|
|ショップの投稿編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/shops/:shop_slug/posts/:id/edit|pvsuwimvsuoitmucvyku/organizations/shops/posts#edit|
|ショップの投稿詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/shops/:shop_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/shops/posts#show|
|ショップの投稿削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/shops/:shop_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/shops/posts#destroy|
|ショップ一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/shops|pvsuwimvsuoitmucvyku/organizations/shops#index|
|ショップ情報編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/shops/:slug/edit|pvsuwimvsuoitmucvyku/organizations/shops#edit|
|ショップ詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/shops/:slug|pvsuwimvsuoitmucvyku/organizations/shops#show|
|ショップ情報更新処理|PATCH/PUT|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/shops/:slug|pvsuwimvsuoitmucvyku/organizations/shops#update|
|ショップ削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/shops/:slug|pvsuwimvsuoitmucvyku/organizations/shops#destroy|
|宿泊施設の投稿を下書きから公開状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hotels/:hotel_slug/posts/:id/to_published|pvsuwimvsuoitmucvyku/organizations/hotels/posts#to_published|
|宿泊施設の投稿を公開から下書き状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hotels/:hotel_slug/posts/:id/to_draft|pvsuwimvsuoitmucvyku/organizations/hotels/posts#to_draft|
|宿泊施設の投稿を公開状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hotels/:hotel_slug/posts/:id/as_published|pvsuwimvsuoitmucvyku/organizations/hotels/posts#as_published|
|宿泊施設の投稿を下書き状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hotels/:hotel_slug/posts/:id/as_draft|pvsuwimvsuoitmucvyku/organizations/hotels/posts#as_draft|
|宿泊施設の投稿一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hotels/:hotel_slug/posts|pvsuwimvsuoitmucvyku/organizations/hotels/posts#index|
|宿泊施設の投稿編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hotels/:hotel_slug/posts/:id/edit|pvsuwimvsuoitmucvyku/organizations/hotels/posts#edit|
|宿泊施設の投稿詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hotels/:hotel_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/hotels/posts#show|
|宿泊施設の投稿削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hotels/:hotel_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/hotels/posts#destroy|
|宿泊施設一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hotels|pvsuwimvsuoitmucvyku/organizations/hotels#index|
|宿泊施設情報編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hotels/:slug/edit|pvsuwimvsuoitmucvyku/organizations/hotels#edit|
|宿泊施設詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hotels/:slug|pvsuwimvsuoitmucvyku/organizations/hotels#show|
|宿泊施設情報更新処理|PATCH/PUT|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hotels/:slug|pvsuwimvsuoitmucvyku/organizations/hotels#update|
|宿泊施設削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hotels/:slug|pvsuwimvsuoitmucvyku/organizations/hotels#destroy|
|アクティビティの投稿を下書きから公開状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/activities/:activity_slug/posts/:id/to_published|pvsuwimvsuoitmucvyku/organizations/activities/posts#to_published|
|アクティビティの投稿を公開から下書き状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/activities/:activity_slug/posts/:id/to_draft|pvsuwimvsuoitmucvyku/organizations/activities/posts#to_draft|
|アクティビティの投稿を公開状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/activities/:activity_slug/posts/:id/as_published|pvsuwimvsuoitmucvyku/organizations/activities/posts#as_published|
|アクティビティの投稿を下書き状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/activities/:activity_slug/posts/:id/as_draft|pvsuwimvsuoitmucvyku/organizations/activities/posts#as_draft|
|アクティビティの投稿一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/activities/:activity_slug/posts|pvsuwimvsuoitmucvyku/organizations/activities/posts#index|
|アクティビティの投稿編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/activities/:activity_slug/posts/:id/edit|pvsuwimvsuoitmucvyku/organizations/activities/posts#edit|
|アクティビティの投稿詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/activities/:activity_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/activities/posts#show|
|アクティビティの投稿削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/activities/:activity_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/activities/posts#destroy|
|アクティビティ一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/activities|pvsuwimvsuoitmucvyku/organizations/activities#index|
|アクティビティ情報編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/activities/:slug/edit|pvsuwimvsuoitmucvyku/organizations/activities#edit|
|アクティビティ詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/activities/:slug|pvsuwimvsuoitmucvyku/organizations/activities#show|
|アクティビティ情報更新処理|PATCH/PUT|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/activities/:slug|pvsuwimvsuoitmucvyku/organizations/activities#update|
|アクティビティ削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/activities/:slug|pvsuwimvsuoitmucvyku/organizations/activities#destroy|
|温泉の投稿を下書きから公開状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id/to_published|pvsuwimvsuoitmucvyku/organizations/hot_springs/posts#to_published|
|温泉の投稿を公開から下書き状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id/to_draft|pvsuwimvsuoitmucvyku/organizations/hot_springs/posts#to_draft|
|温泉の投稿を公開状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id/as_published|pvsuwimvsuoitmucvyku/organizations/hot_springs/posts#as_published|
|温泉の投稿を下書き状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id/as_draft|pvsuwimvsuoitmucvyku/organizations/hot_springs/posts#as_draft|
|温泉の投稿一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts|pvsuwimvsuoitmucvyku/organizations/hot_springs/posts#index|
|温泉の投稿編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id/edit|pvsuwimvsuoitmucvyku/organizations/hot_springs/posts#edit|
|温泉の投稿詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/hot_springs/posts#show|
|温泉の投稿削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hot_springs/:hot_spring_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/hot_springs/posts#destroy|
|温泉一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hot_springs|pvsuwimvsuoitmucvyku/organizations/hot_springs#index|
|温泉情報編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hot_springs/:slug/edit|pvsuwimvsuoitmucvyku/organizations/hot_springs#edit|
|温泉詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hot_springs/:slug|pvsuwimvsuoitmucvyku/organizations/hot_springs#show|
|温泉情報更新処理|PATCH/PUT|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hot_springs/:slug|pvsuwimvsuoitmucvyku/organizations/hot_springs#update|
|温泉削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/hot_springs/:slug|pvsuwimvsuoitmucvyku/organizations/hot_springs#destroy|
|スキー場の投稿を下書きから公開状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id/to_published|pvsuwimvsuoitmucvyku/organizations/ski_areas/posts#to_published|
|スキー場の投稿を公開から下書き状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id/to_draft|pvsuwimvsuoitmucvyku/organizations/ski_areas/posts#to_draft|
|スキー場の投稿を公開状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id/as_published|pvsuwimvsuoitmucvyku/organizations/ski_areas/posts#as_published|
|スキー場の投稿を下書き状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id/as_draft|pvsuwimvsuoitmucvyku/organizations/ski_areas/posts#as_draft|
|スキー場の投稿一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/ski_areas/:ski_area_slug/posts|pvsuwimvsuoitmucvyku/organizations/ski_areas/posts#index|
|スキー場の投稿編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id/edit|pvsuwimvsuoitmucvyku/organizations/ski_areas/posts#edit|
|スキー場の投稿詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/ski_areas/posts#show|
|スキー場の投稿削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/ski_areas/:ski_area_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/ski_areas/posts#destroy|
|スキー場一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/ski_areas|pvsuwimvsuoitmucvyku/organizations/ski_areas#index|
|スキー場情報編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/ski_areas/:slug/edit|pvsuwimvsuoitmucvyku/organizations/ski_areas#edit|
|スキー場詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/ski_areas/:slug|pvsuwimvsuoitmucvyku/organizations/ski_areas#show|
|スキー場情報更新処理|PATCH/PUT|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/ski_areas/:slug|pvsuwimvsuoitmucvyku/organizations/ski_areas#update|
|スキー場削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/ski_areas/:slug|pvsuwimvsuoitmucvyku/organizations/ski_areas#destroy|
|フォトスポットの投稿を下書きから公開状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id/to_published|pvsuwimvsuoitmucvyku/organizations/photo_spots/posts#to_published|
|フォトスポットの投稿を公開から下書き状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id/to_draft|pvsuwimvsuoitmucvyku/organizations/photo_spots/posts#to_draft|
|フォトスポットの投稿を公開状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id/as_published|pvsuwimvsuoitmucvyku/organizations/photo_spots/posts#as_published|
|フォトスポットの投稿を下書き状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id/as_draft|pvsuwimvsuoitmucvyku/organizations/photo_spots/posts#as_draft|
|フォトスポットの投稿一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts|pvsuwimvsuoitmucvyku/organizations/photo_spots/posts#index|
|フォトスポットの投稿編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id/edit|pvsuwimvsuoitmucvyku/organizations/photo_spots/posts#edit|
|フォトスポットの投稿詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/photo_spots/posts#show|
|フォトスポットの投稿削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/photo_spots/:photo_spot_slug/posts/:id|pvsuwimvsuoitmucvyku/organizations/photo_spots/posts#destroy|
|フォトスポット一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/photo_spots|pvsuwimvsuoitmucvyku/organizations/photo_spots#index|
|フォトスポット情報編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/photo_spots/:slug/edit|pvsuwimvsuoitmucvyku/organizations/photo_spots#edit|
|フォトスポット詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/photo_spots/:slug|pvsuwimvsuoitmucvyku/organizations/photo_spots#show|
|フォトスポット情報更新処理|PATCH/PUT|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/photo_spots/:slug|pvsuwimvsuoitmucvyku/organizations/photo_spots#update|
|フォトスポット削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:organization_slug/photo_spots/:slug|pvsuwimvsuoitmucvyku/organizations/photo_spots#destroy|
|組織一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations|pvsuwimvsuoitmucvyku/organizations#index|
|組織情報編集ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:slug/edit|pvsuwimvsuoitmucvyku/organizations#edit|
|組織情報詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organizations/:slug|pvsuwimvsuoitmucvyku/organizations#show|
|組織情報更新処理|PATCH/PUT|/pvsuwimvsuoitmucvyku/organizations/:slug|pvsuwimvsuoitmucvyku/organizations#update|
|組織削除処理|DELETE|/pvsuwimvsuoitmucvyku/organizations/:slug|pvsuwimvsuoitmucvyku/organizations#destroy|
|ユーザ一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/users|pvsuwimvsuoitmucvyku/users#index|
|ユーザ情報編集ページ表示|GET|/pvsuwimvsuoitmucvyku/users/:public_uid/edit|pvsuwimvsuoitmucvyku/users#edit|
|ユーザ情報詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/users/:public_uid|pvsuwimvsuoitmucvyku/users#show|
|ユーザ情報更新処理|PATCH/PUT|/pvsuwimvsuoitmucvyku/users/:public_uid|pvsuwimvsuoitmucvyku/users#update|
|ユーザ削除処理|DELETE|/pvsuwimvsuoitmucvyku/users/:public_uid|pvsuwimvsuoitmucvyku/users#destroy|
|組織登録申請の結果回答処理|POST|/pvsuwimvsuoitmucvyku/organization_registrations/:organization_registration_id/organization_registration_statuses|pvsuwimvsuoitmucvyku/organization_registration_statuses#create|
|組織登録申請一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/organization_registrations|pvsuwimvsuoitmucvyku/organization_registrations#index|
|組織登録申請内容詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/organization_registrations/:id|pvsuwimvsuoitmucvyku/organization_registrations#show|
|お知らせを公開状態で作成する処理|POST|/pvsuwimvsuoitmucvyku/announcements/publish|pvsuwimvsuoitmucvyku/announcements#publish|
|お知らせを下書き状態で作成する処理|POST|/pvsuwimvsuoitmucvyku/announcements/unpublish|pvsuwimvsuoitmucvyku/announcements#unpublish|
|お知らせを下書きから公開状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/announcements/:id/to_published|pvsuwimvsuoitmucvyku/announcements#to_published|
|お知らせを公開から下書き状態へ更新する処理|PATCH|/pvsuwimvsuoitmucvyku/announcements/:id/to_draft|pvsuwimvsuoitmucvyku/announcements#to_draft|
|お知らせを公開状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/announcements/:id/as_published|pvsuwimvsuoitmucvyku/announcements#as_published|
|お知らせを下書き状態のまま更新する処理|PATCH|/pvsuwimvsuoitmucvyku/announcements/:id/as_draft|pvsuwimvsuoitmucvyku/announcements#as_draft|
|お知らせ一覧ページ表示|GET|/pvsuwimvsuoitmucvyku/announcements|pvsuwimvsuoitmucvyku/announcements#index|
|新規お知らせ作成ページ表示|GET|/pvsuwimvsuoitmucvyku/announcements/new|pvsuwimvsuoitmucvyku/announcements#new|
|お知らせ内容編集ページ表示|GET|/pvsuwimvsuoitmucvyku/announcements/:id/edit|pvsuwimvsuoitmucvyku/announcements#edit|
|お知らせ詳細ページ表示|GET|/pvsuwimvsuoitmucvyku/announcements/:id|pvsuwimvsuoitmucvyku/announcements#show|
|お知らせ削除処理|DELETE|/pvsuwimvsuoitmucvyku/announcements/:id|pvsuwimvsuoitmucvyku/announcements#destroy|
