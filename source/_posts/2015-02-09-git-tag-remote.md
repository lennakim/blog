title: git tag/remote的用法
date: 2015-02-08 01:19:59
tags: [git]
---

remote tag的用法总是记不住

#### Git-Remote

```shell
git remote set-url origin <URL>
git remote set-branches [--add] <name> <branch>...
git remote set-url [--push] <name> <newurl> [<oldurl>]
git remote set-url --add <name> <newurl>
git remote set-url --delete <name> <url>
git remote add [shortname] [url] #新建远程仓库

```

#### Git-Tag

``` shell
git tag #列出标签

git tag v0.1.2-light 创建轻量标签

git tag -a v0.1.2 -m "0.1.2 Version" #创建附注标签

git push origin v0.1.2 # 将v0.1.2标签提交到git服务器

git push origin –tags # 将本地所有标签一次性提交到git服务器

git tag -d v0.1.2 # 删除标签

git show v0.1.2  # 用git show命令可以查看标签的版本信息

git tag -a v0.1.1 9fbc3d0 # 给指定的commit打标签

```

## 参考
http://blog.csdn.net/wangjia55/article/details/8793577
http://www.cnblogs.com/wang_yb/p/3867221.html
