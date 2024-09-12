---
title: RubyConfChina2017
date: 2017-09-18 19:08:45
tags: [rails]
---

2017/09/16 本人参加了第九届 rubyconf-china, 从北京特地来到杭州，
2015 年第一次去杭州，那时候一个朋友还在杭州，这次我到杭州，他去别的城市晃荡了。
这次的活动，挺不错，既有十足的干货，也有实际的工程实践，更有很长时间不见的老朋友们。

---

## Day.1 am 第 1 场

Leveraging the power of NGINX with Ruby - tylerdiaz

第一场 是 strikingly 的老外同事分享的 mruby 在 nginx 的应用。
nginx 其实是个很不错的 web 应用，引入 ngx_mruby, 调用 ruby 脚本可以做 json 序列化 xss 过滤等。这样避开了 rails 的 middleware, 跑分性能优秀。而且比起用 cpp 的 ngx_pagespeed, 开发难度小很多。
ngx_mruby 跟 lua 的 OpenResty 相似，只是把 lua 换做 ruby，但是 ngx_mruby 还不能 `require`,这种想法值得关注。

最后结尾：we are hiring

## Day.1 am 第 2 场

Ethereum on Ruby - jan

[jan](https://ruby-china.org/jan) 分享了 ruby 在区块链项目的实践

jan 之前做了开源的 peatio 交易所，分别用 ruby python 实现了 ethumen 的绝大部分功能 . 然后讲了区块链的数据结构，Block, BlockHeader, Merkle Tree, 介绍了 PoW 以及网络层的点对点 tcp 数据传输等。

重点介绍了 ethumen 的虚拟机-- EVM, 一个基于堆栈式的解析器，可以用 EVM 实现智能合约。

目前 jan 成立了 cryptape,  用 rust 开发一个开源的联盟链项目 cita.
最后结尾：we are hiring

很开阔眼界。

## Day.1 pm 第 1 场

Ruby 异步编程奥德赛 - 丁盛豪

dsh0416 分享自己的异步 web 框架 -- midori, 通过 fiber pool 而不是 callback 解决并发问题。
callback 形式会陷入嵌套的地狱，node EventMachine 都不能避免这个问题。

上来 给 thin sinatra express 跑跑分，thin 投机取巧，在 hello world 测试中跑分很高，
一切换到真实的环境，跑分立马下降。原因我记得是在整个请求过程中，不是所有的请求都是异步的，
如果 mysql 请求堵塞了，整个流程就堵塞了。

midori 底层用 fiber 来处理并发以，还优化了中间件，把栈式的压栈弹栈这个循环过程，优化成类似尾递归调用。

作者气氛调动的不错，节奏拿捏的也很好，fiber 的思路很不错。

## Day.1 pm 第 2 场

如何用 Erlang 快速开发 Web 快速开发框架 - bhuztez

听说很多人为了听 B 大演讲专门买了门票。本人也终于见到 B 大的真面目，萌萌的。

B 大说出了至理名言：成功人士都是谈运行效率，失败人士才谈开发效率


讲了 erlang 的一些特性，模式匹配 / 不可变 / 热更新 /parse_transform 等。
开始介绍他的框架 razor, 记得有 url_dispatch peg razor_db 等模块，
很多是通过 pattern matching + parse_transform 实现的，感觉是构造一些解析器，
用到 lex/yacc 的知识。
FP 语言在这方面很强大，推荐个 haskell 项目 https://github.com/haskell/parsec, 总之我是一知半解了。

B 大的这次演讲感觉并不是特别的好，暴露了很多细节，每个细节展开了都是一场演讲，干货密度太高了。

shopping is cheap, let reinvent wheel. 让我们尽情的发明轮子吧


## Day1. pm 第 3 场

Ruby Web 实时通信方案的深度剖析 - 侯俊杰

薄荷网 介绍 ruby 在实时通讯领域的选型，虽然老生常谈了，但有跑分，有每个方案的差异介绍，很不错。

介绍了实时通讯的几个方案 http 轮询方案/ 云服务/ websocket.
重点讲了 websocket 下的几个选择 actioncable /faye-websocket/em-websocket/plezi ,
分别做了跑分，技术上的差异。算是教科书式的选型参考了，演讲的很好。


## Day1. pm 第 4 场

ActiveRecord 源码分析及应用扩展 - Leon

一个 freewhell 的大拿 讲的 ActiveRecode 的实现。
ar 本来就挺复杂，而且开发时间很长。然后用他自己的抽象 -- 变换矩阵/编译器输入输出 巴拉巴拉一些概念
把 ar 又包装了一层。恕本人愚钝，基本没听懂。


## Day1. pm 第 5 场

打造 Ruby 项目的容器化集成工具 - 周艺

彩程 boy 分享的 在前东家的 docker 实践
由公司运维的 docker 翻车史，自己接手后的一步步改进优化，这是个很好的工程师在项目中自我进化例子，
培养完善的逻辑，如何提供解决问题的思路，工程师就是来解决问题的嘛。

虽然大家在群里说 最后都会回归到 k8s, 我只用过 docker, 一直是个凑数的运维，
我挺喜欢这样的工程实践的分享，有了这些摸玻璃渣子过河的经验，才能深刻体会到成熟解决方案的魅力。

---

第一天的分享结束，没随大部队 压西湖，吃了些饭，去旅馆困觉去了。

---

## Day2. am 第 1 场

为 Ruby 设计一款 AOT(Ahead-of-time) 编译器 - 潘旻琦

通过一个 rubyc 工具把 ruby 打包分发，把 rails 项目打包，快速方便的分发。

原理是借鉴 linux 内核的 squash, 剥离出了个用户态的 libsquash, 用 libsqueeze 模拟
出个虚拟内存路径 `__enclose_io_memfs__`,把文件挂载到这个路径下。
不懂，没接触过，涨姿势了。


## Day2. am 第 2 场

爱因斯坦搞炼丹 - Elixir: A Haskeller's Perspective - 祖与占

用 haskell 的视角看 Elixir

本人在 15 年 -16 年看过 <haskell 趣学指南>, 烂尾至今，智商这个东西不说了。
haskell 在 fp 语言中确实有很重要的地位，高配版的 lisp, 很多的 fp 语言从 haskell 借鉴想法。

印象深的讲师举的例子有 F# haskell erlang elixir, 还有 perl

抛了这么张照片

```
有人在说: Elixir只是给erlang包了一层皮.
有人回答: Elixir不单单是给erlang包了一层皮, 他是整个生态的革新.
讲师应了句: Elixir官网还有夜间模式呢.
```

提问有环节，之前有人在 B 大的演讲上 问 模式匹配咋实现的，B 大把锅给了 祖与占，
组与占说："大家可以看下这篇 1987 年的论文，既然时间这么长了，大家应该都能看懂。"
恩，这很 hardcode.

## 随后抽奖环节
3 个人 分一个 btc, 我身边的一个姑娘正是其中之一，
跟机会擦肩而过，愤而离席之，逛逛杭州吧。

---

下面的内容纯属猜测了：

金数据的大神通过机器学习来鉴黄，听说关键字有 "小姨子" ...
充分发挥了大家的热情 提问的时候 每个人都至少 chuai 着 3 个问题
反响热烈 积极响应。哦 对了，听说训练/预测数据 都是用的 python


李亚东讲 mobx 在 rails 前端中的使用，前端我一年不碰了，在此不表。

---

下午 没参加


感观：

这次的 conf，多种语言齐上阵 -- erlang elixir python,
多种主题 -- 区块链 mruby docker 机器学习，可以看到这个社区的包容性 前瞻性。
从之前的 关注 web 开发，到更多的关注性能，rails ruby 的底层探究，在这里都有体现。
rails 已经过了爆发期，正在走向成熟与稳定，正在扩展新的领域。
希望 rubyconf 一直持续下去，越办越好，一直有理由旅个游。

**嗯的重点是，这次参会的妹子比例突破天际了，可是为甚没一个女讲师呢**


PS:

在杭州看到了西西弗书店，也是第一次逛西西弗，买了二本书，带回了关于杭州的一丢丢记忆。

20170918 于杭州开往北京的火车上

---

参考：

https://www.youtube.com/channel/UCOLKFS_uA7nX26_u8z9V9og/playlists 视频

https://2017.rubyconfchina.org/

https://www.zhihu.com/question/65387726/
