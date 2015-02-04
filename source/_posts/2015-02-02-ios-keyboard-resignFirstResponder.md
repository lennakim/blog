title: ios 如何关闭键盘输入
date: 2015-02-02 17:18:55
tags: [ios, keyboard]
---

ios应用在很多时候需要关闭键盘, 记录2种方式.

1 输入完成, 点击某个按钮的时候关闭键盘, 只需要在这个按钮事件调用输入框的 resignFirstResponder

``` object-c
  @IBAction func okTapped(sender: AnyObject) {
    nameTxt.resignFirstResponder() //触发okTapped按钮的事件 关闭键盘
  }
```

2 当手指离开屏幕的时候 关闭键盘, 需要重写touchesEnded

``` object-c
  override func touchesEnded(touches: NSSet, withEvent event: UIEvent) {
    nameTxt.resignFirstResponder() //当手指离开屏幕 关闭键盘
  }
```

---
源码地址 [ViewController.swift](https://github.com/liuningtw/keyboard-resignFirstResponder/blob/master/keyboard-resignFirstResponder/ViewController.swift)

``` object-c
import UIKit

class ViewController: UIViewController {

  @IBOutlet weak var nameTxt: UITextField! //定义输入框
  @IBOutlet weak var resultLab: UILabel! //定义显示框

  override func viewDidLoad() {
    super.viewDidLoad()
    nameTxt.placeholder = "邹倩雯"
  }

  override func didReceiveMemoryWarning() {
    super.didReceiveMemoryWarning()
  }

  override func touchesEnded(touches: NSSet, withEvent event: UIEvent) {
    nameTxt.resignFirstResponder() //当手指离开屏幕 关闭键盘
  }

  @IBAction func okTapped(sender: AnyObject) {
    nameTxt.resignFirstResponder() //触发okTapped按钮的事件 关闭键盘

    resultLab.text = "hi, \(nameTxt.text)"
  }

}

```
