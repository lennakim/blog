title: 使用 vimdiff 作为git diff 工具
date: 2015-04-21 18:38:58
tags: [git, vimdiff]
---

可能是本人 用GUI比较多的缘故, 对默认的 git diff 形式不太直观.
之前用svn的时候 配置过 vimdiff, 所以配置下git的vimdiff.


``` shell
git config --global diff.tool vimdiff # 设置diff工具为 vimdiff

git config --global difftool.prompt false

git config --global alias.d difftool # 设置别名
```

只要输入  `git d`, 感觉是不是更直观了呢?

![](http://7sbqv9.com1.z0.glb.clouddn.com/vimdiff.png)

### 资料

[更换svn diff为vimdiff](http://ccvita.com/445.html)
[Vimdiff 使用](https://www.ibm.com/developerworks/cn/linux/l-vimdiff/)