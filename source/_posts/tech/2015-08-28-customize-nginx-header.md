title: 自定义 nginx 的 header
date: 2015-08-28 17:16:11
tags: [nginx]
---

当你运行 `curl -I ruby-china.com` 查看返回结果

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 1314
Content-Type: text/html; charset=utf-8
Expires: -1
Server: Microsoft-IIS/7.5
X-AspNet-Version: 4.0.30319
p3p: CP="CAO PSA OUR"
X-Powered-By: ASP.NET
Date: Fri, 28 Aug 2015 15:42:00 GMT
```

ruby-china 是用 asp.net 写的?!, 绝不可能吧, 其实这只是用了一个障眼法.

下面马上解密, 前提系统是 ubuntu, 并且已经安装 nginx


### 安装 more_set_headers module
  `sudo apt-get install -y nginx-extras`,
  会安装 [more_set_headers](https://github.com/openresty/headers-more-nginx-module) module

### 设置 nginx.conf 文件
  `sudo vim /etc/nginx/nginx.conf`, 打开 nginx.conf
  在http 结构体中, 加入以下内容:

```
  more_set_headers 'Server: Microsoft-IIS/7.5';
  more_set_headers 'X-AspNet-Version: 4.0.30319';
  more_set_headers 'X-Powered-By: ASP.NET';

```

### 重启 nginx
  `sudo service nginx restart`

### 测试
  curl -I <url>, 看到输出的内容, 已经大功告成.

### 好处
  隐藏真正的 http server, 可以迷惑下菜鸟黑客.

### PS

  原稿写于 2015-06-01, 今天是中元节, 即所谓的鬼节, 没有回老家尽份孝心, 斯人已逝,言犹在耳.
