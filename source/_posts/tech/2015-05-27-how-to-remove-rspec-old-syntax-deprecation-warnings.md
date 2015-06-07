title: 去除rspec should/expect警告
date: 2015-05-27 15:00:44
tags: [rails, rspec]
---

``` ruby
# /spec/spec_helpber.rb
RSpec.configure do |config|
  config.mock_with :rspec do |c|
    c.syntax = [:should, :expect]
  end

  config.expect_with :rspec do |c|
    c.syntax = [:should, :expect]
  end
end
```

## 资料

[How to remove RSpec old syntax deprecation warnings](http://makandracards.com/makandra/25409-how-to-remove-rspec-old-syntax-deprecation-warnings)