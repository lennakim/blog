title: swift 定义各种函数汇总
date: 2015-02-05 00:22:20
tags: [ios, swift]
---

```object-c

// 没有返回值的无参函数
func sayHello() {
  // do something
}

// 返回 string 类型
func sayHello() -> String {
  return "Hi, shooter!"
}

// 一个参数
func sayHello(name: String) -> String {
  // do something
}

// 多个参数
func sayHello(name: String, age: Int) -> String {
  return "Hi, \(name), age is \(age)!"
}

// 参数默认值
func combineName(firstName: String, lastName: String, separator: String = "-") {
    return firstName + separator + lastName
}

// 可变参数
func add(numbers: Int...) -> Int {
  var total = 0
  for i in numbers {
    total += i
  }

  return total
}

// 函数参数别名
func combineName(firstName first: String, lastName last: String) {
    // accessing the parameters can be done by referencing
    // "first" and "last" respectively
    return first + " " + last;
}

var fullName = combineName(firstName: "Steve", lastName: "Wozniak")

```

### 参考

[C#与Swift的函数比较](http://www.swiftmi.com/topic/50.html)
