title: rails alias_method_chain 的用法
date: 2015-08-16 13:06:07
tags: [rails, ruby]
---

其实 alias alias_method 已经把我弄晕了.

### 先说 alias alias_method

```ruby
class User

  def name
    puts "user name is Johnnie Walker"
  end

  def mobile
    puts "user mobile is 186-1111-1111"
  end

  def self.add_alias
    alias alias_mobile mobile
    alias_method :alias_name, :name
    # 另一种写法
    # alias :alias_mobile :mobile
    # alias_method 'alias_name', 'name'
  end

  add_alias
end

class Developer < User

  def name
    puts "developer name is Linus Torvalds"
  end

  def mobile
    puts "developer mobile is 186-9999-9999"
  end

  add_alias
end

user = User.new
dev = Developer.new

dev.alias_mobile  # => user mobile is 186-1111-1111
user.alias_mobile # => user mobile is 186-1111-1111
puts "-" * 20
dev.alias_name  # => developer name is Linus Torvalds
user.alias_name # => user name is Johnnie Walker

```

语法层面的差异可以忽略,  new_name old_name 的顺序总是弄混.

在继承关系中, alias_name 的内容被重写, alias_mobile并没有.

This is because alias is a keyword and it is lexically scoped. It means it treats self as the value of self at the time the source code was read . In contrast alias_method treats self as the value determined at the run time.

### alias_method_chain

alias_method_chain 是 **ActiveSupport** 的一个公有实例方法,
同样接受两个参数, 可以是符号, 也可以是字符串, 但第1个参数是原始方法,
alias_method的第2个参数是原始方法, 晕~.

```ruby

class Car < ActiveRecord::Base
  class << self
    #先将find方法别名
    alias find_without_args find

    #再定义find args 方法
    def find_with_args(*args)
      p "调用find之前"
      find_without_args
      # 调用find_without_args 其实就是find方法
      p "调用find之后"
    end

    alias find find_with_args
  end
end

Car.find(:mustang)
#实际调用find_with_args, 在find_with_args方法中,
#又再调用了find_without_args, 也就是原生的find方法了.
```
其实 alias_method_chain 只是做了个 dsl

```ruby
alias_method_chain :find, :args
#相当于
alias find_with_args find
alias find find_without_args
```

### 资料
[In Defense of Alias](http://erniemiller.org/2014/10/23/in-defense-of-alias/)
[alias vs alias_method](http://blog.bigbinary.com/2012/01/08/alias-vs-alias-method.html)
[rails alias_method_chain rails3](http://zires.info/2010/12/rails-alias_method_chain-rails3/)
[Should I use alias or alias_method](http://stackoverflow.com/questions/4763121/should-i-use-alias-or-alias-method)
