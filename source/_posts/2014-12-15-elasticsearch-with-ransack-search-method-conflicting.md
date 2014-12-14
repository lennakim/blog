title: Elasticsearch 与 Ransack 的 search 方法冲突
date: 2014-12-15 14:36:28
tags: rails elasticsearch ransack
---

最近在项目中用 [Elasticsearch](http://www.elasticsearch.org/) 做全文搜索,
由于在之前用到 [Ransack](https://github.com/activerecord-hackery/ransack) 做模糊搜索,
这2个gem都在model中添加了 `search` 方法,一起使用会造成冲突.

于是找到一个解决办法 [es-rails-issues-96](https://github.com/elasticsearch/elasticsearch-rails/issues/96).

1 引入gem

```ruby
gem "ransack"
gem "elasticsearch-model"
gem "elasticsearch-rails"
```

2 include Elasticsearch::Model

``` ruby
# /models/article.rb

class Article < ActiveRecord::Base
  include Elasticsearch::Model
end
```

`Article.search`可以使用了, 由于上边说到的原因,  Elasticsearch search 方法会被 Ransack覆盖.

3 解决办法

```ruby
# /models/article.rb

def self.search_with_es(*args)
  __elasticsearch__.search(*args)
end
```

使用 `Article.search_with_es` 即可.

