title: "升级hexo"
date: 2015-05-03 21:25:55
tags: [hexo]
---

最近换了一个Mac pro本子, 把原来的blog项目导入到新本子中, 发现不能run了.
到官方代码仓库看了下, 作者已经升级hexo, 现在pro安装的hexo版本比较高.
[Breaking Changes in Hexo 3.0](https://github.com/hexojs/hexo/wiki/Breaking-Changes-in-Hexo-3.0), 从题目上看, 作者也是蛮狠的.

升级hexo, 请戳 [Migrating from 2.x to 3.0](https://github.com/hexojs/hexo/wiki/Migrating-from-2.x-to-3.0)

在这里纪下我的升级步骤


#### First

修改 ./package.json

```
{
  "hexo": {
    "version": ""
  }
}
```

#### Second

安装hexo组件

```
npm install hexo-cli -g
npm install hexo --save

```

安装生成器

```
npm install hexo-generator-index --save
npm install hexo-generator-archive --save
npm install hexo-generator-category --save
npm install hexo-generator-tag --save
```

安装server

```
npm install hexo-server --save
```

#### Third

安装部署工具, 由于我用github page, 只用安装hexo-deployer-git

```
npm install hexo-deployer-git --save

```

升级各种插件

```
npm install hexo-renderer-marked@0.2 --save
npm install hexo-renderer-stylus@0.2 --save
npm install hexo-generator-feed@1 --save
npm install hexo-generator-sitemap@1 --save
```

最后不要忘了这个

```
npm install hexo-renderer-ejs --save

```

不装 ejs 会出现[hexo-issues-632](https://github.com/hexojs/hexo/issues/632)描述的问题