title: 查找 mysql socket 文件位置
date: 2015-01-07 10:44:54
tags: [mysql, Mac]
---

Mac os 运行一个rails项目, 经常有找不到 mysql socket文件的问题, 在stackoverflow上
找到了解决办法 -- [cannot-find-mysql-sock](http://stackoverflow.com/questions/748478/cannot-find-mysql-sock) .

于是发现一个灰常简单的的命令 **mysql_config --socket**

```
mysql_config --socket

=> /tmp/mysql.sock

```

迎刃而解, 只是感觉这个命令太偏门了.