title: 从grape中获取header数据
date: 2014-07-18 18:04:15
tags: [ruby,rails,grape]
---

[grape](https://github.com/intridea/grape) 是一个方便创建 REST-like APIs的gem.

client将一些元数据存在header中, 需要从grape中获取header数据, 得到version版本, 直接上代码.

```ruby
  def get_client_version
    request = Grape::Request.new(env)
    headers = request.headers
    version = headers['X-Version'].to_s
  end

```