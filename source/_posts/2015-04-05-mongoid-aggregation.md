title: mongoid 聚合功能
date: 2015-04-05 18:32:21
tags: [mongoid, aggregation, mapreduce]
---

### querying 查询

忽略某些字段的查询用 `without`, 只查询某些字段可以用 `only`.

```
class User
  include Mongoid::Document
  include Mongoid::Timestamps

  field :name,   type: String
  field :email,  type: String
  field :gender, type: String

end

User.without(:name)
User.without(:name, :gender)
User.only(:name)
User.only(:name, :email)

```

### aggregation 聚合

#### group
我们有时需要 类似sql的group功能 , mongoid 提供了对mongoDB aggregate的支持,
这样可以使用 mongoDB的 [$group](http://docs.mongodb.org/manual/reference/method/db.collection.group/) 函数了.


``` ruby
class User
  include Mongoid::Document
  include Mongoid::Timestamps

  def self.added_fans(day_num)

    self.collection.aggregate(
      {
        "$match" => {
          "followable_type" => "User",
           "created_at" => {
              "$gte" => yesterday.to_i.days.ago.beginning_of_day, # 大于等于 昨天的开始时间
              "$lte" => Date.yesterday.end_of_day # 小于等于 昨天的结束的时间
           }
        }
      }, # 查询条件
      {
        "$group" => {
          _id: "$follow_id", # 根据 follow_id 分组统计
          matches: { "$sum" => 1 } # 统计数量
        }
      },
      {
        "$sort" => { matches: -1 } #倒序
      },
      {
        "$limit" => 10
      }
    )
  end

end

```

#### [map_reduce](http://mongoid.org/en/mongoid/docs/querying.html#map_reduce)

map_reduce

```ruby
class Band

  def self.likes_count
    map = %Q{
      function() {
        emit(this.name, { likes: this.likes }); # 发送 name 与 likes
      }
    }

    reduce = %Q{
      function(key, values) {
        var result = { likes: 0 };

        values.forEach(function(value) {

          result.likes += value.likes; # 获得value.likes 并 累加

        });

        return result; #输出结果
      }
    }

    map_reduce(map, reduce).out(inline: true)
  end
end

Band.likes_count

```

MapReduce概念可以查看[wiki](http://zh.wikipedia.org/zh/MapReduce)
或者[知乎](http://www.zhihu.com/question/23345991)