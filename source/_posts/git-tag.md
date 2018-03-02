---
title: git tag
date: 2017-03-29 13:23:52
category: [工具]
tags: [git]
---
# 主要操作：
## 创建附注标签
```
$ git tag -a v0.1.2 -m “0.1.2版本”
```
## 删除标签
误打或需要修改标签时，需要先将标签删除，再打新标签。
```
$ git tag -d v0.1.2 # 删除标签
```
## 将v0.1.2标签提交到git服务器
```
$ git push origin v0.1.2
```
## 将本地所有标签一次性提交到git服务器
```
$ git push origin --tags
```

# 列出标签
```
$ git tag # 在控制台打印出当前仓库的所有标签
$ git tag -l ‘v0.1.*’ # 搜索符合模式的标签
```
# 打标签
git标签分为两种类型：轻量标签和附注标签。轻量标签是指向提交对象的引用，附注标签则是仓库中的一个独立对象。建议使用附注标签。
## 创建轻量标签
```
$ git tag v0.1.2-light
```
## 创建附注标签
```
$ git tag -a v0.1.2 -m “0.1.2版本”
```
创建轻量标签不需要传递参数，直接指定标签名称即可。
创建附注标签时，参数a即annotated的缩写，指定标签类型，后附标签名。参数m指定标签说明，说明信息会保存在标签对象中。

# 切换到标签
与切换分支命令相同
```
$ git checkout [tagname]
```
# 查看标签信息
用git show命令可以查看标签的版本信息：
```
$ git show v0.1.2
```
# 删除标签
误打或需要修改标签时，需要先将标签删除，再打新标签。
```
$ git tag -d v0.1.2 # 删除标签
```
参数d即delete的缩写，意为删除其后指定的标签。

# 给指定的commit打标签
打标签不必要在head之上，也可在之前的版本上打，这需要你知道某个提交对象的校验和（通过git log获取）。
# 补打标签
```
$ git tag -a v0.1.1 9fbc3d0
```

标签发布
通常的git push不会将标签对象提交到git服务器，我们需要进行显式的操作：
```
$ git push origin v0.1.2 # 将v0.1.2标签提交到git服务器
$ git push origin --tags # 将本地所有标签一次性提到git服务器
```
注意：如果想看之前某个标签状态下的文件，可以这样操作
1. git tag   查看当前分支下的标签

2. git  checkout v0.21   此时会指向打v0.21标签时的代码状态，（但现在处于一个空的分支上）

3. cat  test.txt   查看某个文件

refer to：http://www.csser.com/dev/580.html