title: Linux下查找并批量修改文件扩展名
date: 2015-09-20 10:23:04
tags: [linux, shell]
---

Linux下查找并批量修改文件扩展名

http://www.cnblogs.com/knows/archive/2013/01/02/2842489.html


http://www.ahlinux.com/start/cmd/498.html



find ./ -type f -name "*.less" | xargs  rename "s/less/scss/“


find ./ -type f -name "*.po"  | xargs  -I {} cp {} <new_path> #复制

http://bbs.chinaunix.net/thread-525576-1-1.html