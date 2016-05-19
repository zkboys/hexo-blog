---
title: MongoDB-从懵逼到入门
date: 2016-05-19 21:50:53
category: [后端, 数据库]
tags: [mongodb]
toc: true
---
## 安装
根据[官网](https://docs.mongodb.com/manual/installation/)进行安装。

[ubuntu 15 安装完成之后无法使用解决办法](http://askubuntu.com/questions/617097/mongodb-2-6-does-not-start-on-ubuntu-15-04)：
```
sudo apt-get install upstart-sysv
重启之后，就可以使用了。
```
## 常用shell命令
- 查看当前数据库：`db`
- 查看有那些数据库：`show dbs`
- 切换数据库：`use db_name`
- 查看集合：`show collections`
- 查询：`db.collection_name.find()`
- 插入：`db.collection_name.insert(obj)`
- 更新：`db.collection_name.update(condition,newObj)`
