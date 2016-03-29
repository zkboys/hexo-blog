---
title: 本地新建文件夹并提交到github上
date: 2016-03-17 14:56:35
category: [工具]
tags: [github]
---
先手动在github官网上创建一个空的仓库,名为repo-name

方法一:通过命令clone到本地,一般是还没有写任何代码,clone下来之后再写内容
```
  git clone git@github.com:your-name/repo-name.git
  or
  git clone https://github.com/your-name/repo-name.git
```
注意:https方式ssh-key不起作用,每次push都要输入账号密码

方法二:本地已经写好文件了,然后才创建的github仓库。
```
cd 到本地文件夹
git init
git add --all
git commit -m "first commit"
git remote add origin git@github.com:your-name/repo-name.git
git push -u origin master
```

## 编辑完成之后，提交命令
```
git add --all
git commit -m '这里写注释'
git push origin master
```
