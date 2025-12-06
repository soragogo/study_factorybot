## build
`build`戦略は、DBへの保存を行わず、メモリ上にインスタンスを作成する

### 基本的な使用例
まず、前提となるFactory定義があるとする。

```ruby
# test/factories/users.rb
FactoryBot.define do
  factory :user do
    name { "Jane Doe" }
    email { "jane@example.com" }
    # 関連付け (Postモデルがあると仮定)
    association :latest_post, factory: :post
  end

  factory :post do
    title { "Hello World" }
  end
end
```

この定義を使って呼び出す。

```ruby
# インスタンスを作成（DBには保存されない）
user = FactoryBot.build(:user)

puts user.name # => "Jane Doe

# DBには保存されていないので、IDはnilになる
puts user.id

# まだ保存されていないレコードか？
puts user.new_record? # => true
```

### association（関連付け）の挙動
`build`戦略を使うと、関連づけられたオブジェクトも`build`戦略で作られる。

### build_listの使い方
`build_list`は、指定した個数のインスタンスをbuildして配列として返すメソッド。
一度に複数のオブジェクトをテストデータとして用意したい時に使える。

```ruby
users = FactoryBot.build_list(:user, 3)

puts users.class       # => Array
puts users.size        # => 3
puts users[0].name     # => "Jane Doe" (Factoryのデフォルト値)

# すべて DB未保存
puts users.all?(&:new_record?) # => true
```

また、build_listはブロックを受け取ることができる。
ブロック引数に渡されるのは、
1. 生成されたオブジェクト(`user`)
2. インデックス番号

これを使うと、連番のデータを手動で作成できる

```ruby
users = FactoryBot.build_list(:user, 3) do |user, i|
  user.email = "person_#{i}@example.com"
  user.is_special = true if i.even?
end

puts users[0].email # => "person_0@example.com"
puts users[1].email # => "person_1@example.com"
```