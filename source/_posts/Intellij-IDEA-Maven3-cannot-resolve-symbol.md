---
title: Intellij IDEA Maven3 cannot resolve symbol
date: 2016-03-21 19:29:13
category: [工具]
tags: [错误]
---
Intellij IDEA + Maven3 模块无法引入得问题，编辑器上显示红色下滑线，maven可以正常编译项目，项目也可以运行，就是编辑器有红色得提示，碍眼。网上搜索了一些解决办法，但是没什么鸟用。那就应该是缓存问题，清理一下重启Idea就Ok了：
```
File -> Invalidate Caches/Restart...
```
