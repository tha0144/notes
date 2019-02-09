# 電脳本棚

## 基本的な機能

* ログイン機能
    + 他のユーザーをフォロー可能（後でいいか）
    + ジャンルをフォロー
* 本（書籍名・著者名・出版社名・ジャンル）を登録。
    + 自分用のコメントを付けれる。
    + 既所持のものも登録可能。この場合、書評を付けれる。
    + 登録した本は公開/非公開が選べる。非公開の場合、他のユーザーには見えない（検索結果にも出ない）
* 

## テーブル(DB)

* users
    + name
    + email
    + password
    + introduction
* books
    + title
    + author
    + publisher
    + published_at
    + category_id
    + user_id
    + possession (所持・非所持)
    + is_open → 公開/非公開
    + comment → コメント、非公開
    + review → 書評、公開される
* categories
    + name
* tags
    + name
* user_follow
    + user_id
    + follow_id
* favorites
    + user_id
    + book_id
    + comment
* category_follow
    + user_id
    + category_id

## ルーター

* 非ログイン時
    + ユーザー登録
    + ログイン
* ログイン時
    + ユーザーホーム（仮称）画面表示
    + 本の検索
    + ユーザーフォロー
    + ふぁぼ
    + ジャンルフォロー
    

## モデル

* User
    + fillable(name, email, password)
    + hidden(password, remember_token)
    + books: 登録した本一覧 // hasMany->Book  
        // ユーザーフォロー機能（後にする？）
    + followings: 自分がフォローしたユーザー一覧 // belongsToMany->User
    + followers: 自分をフォローしているユーザー一覧 // belongsToMany->User
    + followQ: 自分がそのユーザーをフォローしているかどうか(boolean)
    + follow: そのユーザーをフォローする
    + unfollow: そのユーザーのフォローを解除する  
        // ふぁぼ機能
    + favorites: ふぁぼした本一覧 // belongsToMany->Book
    + favoriteQ: 自分がその本をふぁぼしているかどうか(boolean)
    + favorite: その本をふぁぼする
    + unfavorite: その本のふぁぼを解除する  
        // カテゴリーフォロー
    + following_categories: フォローしているカテゴリー一覧 // belongsToMany->Category
    + followQ_category: そのカテゴリーをフォローしているか(boolean)
    + 
* Book
    + fillable(title, user_id, is_open)
    + user: 登録したユーザー // belongsTo->User
    + favorite_users: ふぁぼしたユーザー一覧 // belongsToMany->User
    + category: 付与されたカテゴリー // belongsTo->Category
* Category
    + fillable(name)
    + follow_users: そのカテゴリーをフォローしているユーザー一覧 // belongsToMany->User
    + books_in_category: そのカテゴリーを付与された書籍一覧 // hasMany->Book
* Tag
    + fillable(name)
    + tagged_books: そのタグを付与された書籍の一覧 // belongsToMany->Book

## コントローラー

* UsersController
    + 
* BooksController
    + 
* UserFollowController
    + 
* FavoritesController
    + 

## ビューアー

## 検討中事案

* ジャンル  
    カテゴリーとタグに分ける？  
    こちらで指定リストを用意するカテゴリーと、ユーザー側で自由に（個数制限あり）付けられるタグ
* 出版社  
    publishersテーブルを用意し、booksテーブルではpublisher_idで管理？  
    詳細検索画面でもpulishersテーブルに登録された出版社をドロップダウン形式で表示？
* 将来的に  
    ユーザーと書籍を切り離したい（書籍情報はISBNから引っ張って来れないか）
* スマホアプリ  
    OCR機能搭載のスマホアプリなんかを使って、書店で表紙を撮影→情報登録/既所持or非所持の判定等もできるようにしたい

## 検討済事案

* ふぁぼ機能  
    ふぁぼした本に自分用のコメントを付けるとすると、本来の登録者のコメントとの区別が必要。  
    Favoriteレコードに自分のコメント（書評も）も付けられるようにする。  
    自分が投稿したものとしてBookレコードを新規作成すると、検索の邪魔になる。