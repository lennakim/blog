title: inherit_resources 添加分页功能
date: 2015-03-10 13:16:44
tags: [ruby, gem, pagination]
---

[inherited_resources](https://github.com/josevalim/inherited_resources) 可以为controller 自动添加 action.
[kaminari](https://github.com/amatsuda/kaminari)是常用的分页插件.
inherited_resources 默认的 `index action` 是没有分页功能的, 这是个灾难, 添加以下代码为 index 实现分页.

```ruby
class Car < ActiveRecord::Base
  scope :recent, -> {order(created_at: :desc)}
end
```

```ruby
class CarsController < ApplicationController

  inherit_resources

  protected

  def collection
    end_of_association_chain.recent.page(params[:page])
  end

end

```

### 资料

[Kaminari work with Inherited Resources](http://stackoverflow.com/questions/21258436/does-kaminari-work-with-inherited-resources)
