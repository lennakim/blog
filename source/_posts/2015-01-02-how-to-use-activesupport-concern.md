title: 如何使用 ActiveSupport::Concern
date: 2015-01-02 23:38:11
tags: [rails, active_support]
---

在使用[es-model](https://github.com/elasticsearch/elasticsearch-rails/)的时候, include Elasticsearch::Model, model 就有了search方法, 代码如下:

``` ruby /models/article.rb
class Article < ActiveRecord::Base
  include Elasticsearch::Model
end

Article.search # is worked

```

如何通过ActiveSupport::Concern, 实现类似的功能呢?

```ruby test.rb
require 'active_support'

module Foo
  extend ActiveSupport::Concern

  def instance_method
    puts "this is a instance_method"
  end

  included do
   ## 定义类方法
    def self.class_method
      puts "this is a class_method"
    end
  end
end

class Test
  include Foo
end

Test.new.instance_method
Test.class_method

```

campo有[相似代码](https://github.com/chloerei/campo/blob/master/app/models/concerns/likeable.rb)

```ruby

module Likeable
  extend ActiveSupport::Concern

  included do
    has_many :likes, as: 'likeable', dependent: :delete_all
  end

  def liked_by?(user)
    likes.where(user: user).exists?
  end
end

```

这样的好处是: **1. 代码复用**  **2. 分拆代码, 使结构更清晰**.


AS::Concern的另一个作用: 解决modules之间的dependencies, 可以参考 ihower的[文章](https://ihower.tw/blog/archives/3949).

