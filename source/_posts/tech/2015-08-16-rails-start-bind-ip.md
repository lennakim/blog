title: rails启动时绑定ip
date: 2015-07-26 01:25:48
tags: [rails]
---

Rails 在升级到4.2后, 使用 `rails s` 运行程序后, 不再监听 0.0.0.0 端口.
导致 http://localhost:3000, http://127.0.0.1:3000 可以正常访问,
当使用 http://192.168.1.xx:3000/ 的时候, 访问不到 rails 程序.

### 解决

1 在启动 rails 的时候 绑定ip

  `rails s -b 0.0.0.0`
  可以给这条命令指定一个 alias,
  `alias rsb="rails s -b 0.0.0.0"`

2 修改 default_options

```
# /config/boot.rb
module Rails
  class Server
    def default_options
      super.merge(Host: '0.0.0.0', Port: 3000)
    end
  end
end
```

### 资料

[How to change the default binding ip of Rails 4.2 development server](http://stackoverflow.com/a/29562898/1240067)

[Make Rails 4.2 server listens to all interfaces](https://fullstacknotes.com/make-rails-4-2-listen-to-all-interface/)
