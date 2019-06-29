---
title: "Hello world"
data: 2019-1-6-29   
categories: C++
tags:
- R包
- R
- roxygen2
- 软件包开发
---

Github地址：<https://github.com/ShixiangWang/learn-devel-Rpkg>

内容源自《R实战》第二版，酌情删改。

## 写在阅读之前

如果你想要的是快速构建R包骨架，推荐阅读[在巨人的肩膀前行 催化R包开发](http://blog.fens.me/r-package-faster/)进行学习；如果你想了解更为基本的R包创建知识和过程，推荐阅读[开发自己的R包sayHello](http://blog.fens.me/r-build-package/)、谢益辉写的[编写R包](https://bookdown.org/yihui/r-ninja/r-package.html)章节以及本文[创建包的文档](#document-pkg)和[建立包](#build-pkg)章节。阅读一篇文档就想写好R包是远远不够的，还需要不断地实战和理解，才能融会贯通。不仅如此，一些函数和文档写法、技巧也是值得学习的，这正是本文的价值所在。

Let's begin!