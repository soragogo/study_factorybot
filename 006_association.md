## Association(関連付け)
factory_botでは、他のファクトリとの関連付けを定義することができる。
`association`メソッドは、そのために使用される。

### 使い方（構文）
```ruby
association :name, factory: :factory_name, strategy: :build_strategy, ...
```
###　「関連づいている」ってどういう状態？
2つのデータがIDを通じて繋がっている状態。
build戦略では、idが付与されていないが、例えばauthorとpostが関連づいているとするのなら、

post.author # => author

のようにくっついてる状態になる。

定義の仕方としては、以下のようにできる（どっちでもいい）

### 暗黙的な定義
```ruby
factory :post do
  # ...
  author
end
```

### 明示的な定義
```ruby
factory :post do
  # ...
  association :author, factory: :author
```
また、factory: :xxx を使えば明示的にファクトリ名を指定できるし、指定しない場合はそのまま属性名が使われる。

### インライン定義
関連付けられたオブジェクトをすぐ使用したい時など
```ruby
factory :post do
  # ...
  author { association : author }
end
```

### 属性の上書き
関連付けられたオブジェクトの特定の属性を上書きしたい時
factory :post do
  # ...
  association :author, factory: :user, last_name: "Writely"
end

### 関連付けの上書き
`build`や`create`を呼び出す際に、関連付けられたオブジェクトを渡すことで、定義された関連付けを上書きすることができる。
```ruby
post = build(:post, author: new_author)
```