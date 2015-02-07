title: swift扩展-extension
date: 2015-02-08 00:44:58
tags: [swift, ios, ruby]
---

swift 有一个特别的关键字 -- **extension**


```object-c
extension Double{
  var km: Double { return self * 1_000.0 }
  var m:  Double { return self }
  var cm: Double { return self / 100.0 }
  var mm: Double { return self / 1_000.0 }
  var ft: Double { return self / 3.28084 }
}

let oneInch = 25.4.mm
println("One inch is \(oneInch) meters")

let aMarathon = 42.km + 195.m
println("Amarathon is \(aMarathon) meters long")
```

马上想到的是 ruby monkey-patch

```ruby
class Fixnum

  def seconds
    return self
  end

  def minutes
    return self*60
  end

  def days
    return self*60*60
  end
end
############
5.seconds
2.minutes
1.days

```

---

在ios的例子中 [ViewControllerExtensions](https://github.com/liuningtw/ruby-china_ios/blob/master/ruby-china_ios/ViewControllerExtension.swift) 扩展ViewController, 继承 **UITableViewDataSource** , 并实现 **protocol** ,

类似ruby中用 module 扩展class.


### 参考
[Swift扩展-Extension](http://blog.csdn.net/tonny_guan/article/details/36198911)
