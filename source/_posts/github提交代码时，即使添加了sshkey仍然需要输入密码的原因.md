---
title: github提交代码时，即使添加了ssh-key仍然需要输入密码的原因
date: 2016-03-10 13:21:05
category: [工具]
tags: [github, push, ssh-key]
---
原因是库克隆下来的时候使用的是https的方式，改用ssh方式就OK了,

将https方式改为ssh方式：
```
git remote rm origin
git remote add origin git@github.com:yourusername/demo.git
git push origin
```
git clone　时，尽量使用ssh方式．


ssh-key生成方式：[戳这里](https://help.github.com/articles/generating-an-ssh-key/)
