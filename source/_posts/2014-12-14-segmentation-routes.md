title: 分割rails中的routes文件
date: 2014-12-14 11:08:09
tags: [rails, routes]
---

在rails项目中有一个非常重要的文件 `routes.rb`, 管理rails的请求路径.
在随着项目的膨胀, routes.rb 会越来越大, 分割routes会使目录结构更加清晰.

---

1 先在 config 下新建 routes 文件夹,
2 然后将routes.rb 拆分放到不同的文件夹内,
3 再然后加载拆分后的文件, 有两种方式:

#### 第一种

在 `config/routes.rb` 中定义 `draw` Method:

```ruby
class ActionDispatch::Routing::Mapper
  def draw(routes_name)
  instance_eval(File.read(Rails.root.join("config/routes/#{routes_name}.rb")))
  end
end

draw :admin
```

#### 第二种

更改 `application.rb` 的 `load path`

```ruby
config.paths["config/routes"] += Dir[Rails.root.join("config/routes/*.rb")]
```

如果你的 routes 非常依赖顺序, 需要逐步加载文件

```ruby
# 逐个加载
config.paths.config.routes << File.join(Rails.root, "config/routes/routes_01.rb")
config.paths.config.routes << File.join(Rails.root, "config/routes/routes_02.rb")
config.paths.config.routes << File.join(Rails.root, "config/routes/routes_03.rb")

```

