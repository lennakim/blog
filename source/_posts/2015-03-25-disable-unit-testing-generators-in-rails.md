title: rails中禁掉某些生成器
date: 2015-03-25 20:13:45
tags: [rails generators]
---

在用rails创建项目的时候, 有时候有生成一些 help_spec view_spec 文件, 在实际项目中这些文件
基本不会用到, 可以禁用某些 generators, 不在生成  help_spec view_spec文件.

```ruby
  # /config/application.rb

  config.generators do |g|
    g.test_framework  :rspec, fixture: false
    g.view_specs      false
    g.helper_specs    false
  end
```