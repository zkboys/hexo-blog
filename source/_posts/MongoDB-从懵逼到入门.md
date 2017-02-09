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
## 启动&停止
官网上有相关文档，一切以官网为主
### 终端方式
```
# 启动
mongod
# 停止
关闭当前终端即可
```
### 后台运行方式
```
# 启动 添加--fork参数 --logpath：指定日志文件 --logappend：日志以追加方式记录
mongod --fork --logpath /var/log/mongodb.log --logappend

# 停止 通过admin数据库命令停止
mongo
use admin
db.shutdownServer()
```

## 卸载
[http://askubuntu.com/questions/147135/how-can-i-uninstall-mongodb-and-reinstall-the-latest-version](http://askubuntu.com/questions/147135/how-can-i-uninstall-mongodb-and-reinstall-the-latest-version)
```
sudo apt-get purge mongodb mongodb-clients mongodb-server mongodb-dev
sudo apt-get purge mongodb-10gen
sudo apt-get autoremove
```


## 常用shell命令
- 查看当前数据库：`db`
- 查看有那些数据库：`show dbs`
- 切换数据库：`use db_name`
- 查看集合：`show collections`
- 查询：`db.collection_name.find()`
- 插入：`db.collection_name.insert(obj)`
- 更新：`db.collection_name.update(condition,newObj)`

## 导入导出
[更多参考这里](http://www.jb51.net/article/52498.htm)

```
导出数据库：
mongodump -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 -o 保存导出文件路径

如果没有用户密码，可以去掉-u和-p。
如果导出本机的数据库，可以去掉-h。
如果是默认端口，可以去掉--port。
如果想导出所有数据库，可以去掉-d。

导入数据库：
mongorestore -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 --drop 文件存在路径

--drop的意思是，先删除所有的记录，然后恢复

导出表：
mongoexport -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 -c 表名 -f 字段 -q 条件导出 --csv -o 文件名

-f 导出指字段，以字号分割，-f name,email,age导出name,email,age这三个字段
-q 可以根查询条件导出，-q '{ "uid" : "100" }' 导出uid为100的数据
--csv 表示导出的文件格式为csv的，这个比较有用，因为大部分的关系型数据库都是支持csv，在这里有共同点

导入表：
1.1,还原整表导出的非csv文件
mongoimport -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 -c 表名 --upsert --drop 文件名  
重点说一下--upsert，其他参数上面的命令已有提到，--upsert 插入或者更新现有数据

1.2,还原部分字段的导出文件
mongoimport -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 -c 表名 --upsertFields 字段 --drop 文件名  
--upsertFields根--upsert一样

1.3,还原导出的csv文件
mongoimport -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 -c 表名 --type 类型 --headerline --upsert --drop 文件名  
上面三种情况，还可以有其他排列组合的。

```
