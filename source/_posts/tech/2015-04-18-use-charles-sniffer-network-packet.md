title: 使用 charles 抓取网络包
date: 2015-04-18 19:40:44
tags: [charles, sniffer]
---

最近一直在做 api server, 有时候也需要分析手机App的网络请求, 之前在win环境下一直用 fiddler
做这样的工作, 然后在 mac下发现了[Charles](http://www.charlesproxy.com/), 样子是个花瓶, 不过功能很强大哦.

说下步骤

1 确保手机和mac在同一个局域网

2 设置Charles代理, Proxy -> Proxy Settings, 保持默认即可, 记住端口 8888

![](http://7sbqv9.com1.z0.glb.clouddn.com/charles-proxy-settings.png)

3 查看mac 本地ip

  ```shell
    ifconfig |grep inet

      inet6 ::1 prefixlen 128
      inet 127.0.0.1 netmask 0xff000000
      inet6 fe07::1%lo0 prefixlen 64 scopeid 0x1
      inet6 fe07::9e40:8ff:fe9d:2136%en0 prefixlen 64 scopeid 0x4
      inet 192.168.1.109 netmask 0xffffff00 broadcast 192.168.1.205
  ```
  本地 ip地址是  192.168.1.109

4 设置手机

设置 -> 无线局域网 -> 点蓝色的info图标, 找到 http 代理

服务器 输入mac本地ip `192.168.1.109`, 端口输入 `8888`

![](http://7sbqv9.com1.z0.glb.clouddn.com/ios-proxy.jpg)

5 charles 会提示弹窗 , allow 即可.

在左侧栏, 就可以看到请求的连接了.

---

另外 charles 可以模拟网络速度, 很贴心, 通过 Proxy-> Throtting Settings

![](http://7sbqv9.com1.z0.glb.clouddn.com/charles-throtting-settings.png)

PS 免费版 charles 会有些限制.

### 资料
[fiddler](http://www.telerik.com/fiddler)
[wireshark](https://www.wireshark.org/)
[使用charles来抓取手机App的网络包](http://www.baidufe.com/item/8a53eea855cb6289993f.html)
