---
title: 使用node创建一个命令行工具 zk-init
date: 2016-04-14 11:49:12
category: [工具]
tags: node
---
## 安装
```
$ sudo npm install zk-init -g
```
## 使用
```
$ zk-init [template name]
```
在终端输入一个命令就能执行相关的操作，比如终端输入`$ zk-init`，就会的一个简单的`jQuery`开发的demo。输入`$ zk-init jquery-webpack`就会得到一个通过`webpack`构建得jQuery项目初始结构。

做这个小工具主要是学习一下“手脚架”是怎么写的。同时也想通过这个工具快速初始化出各种项目结构，比如我要写一个小demo的时候，需要新建一个文件夹，然后再创建`html`，`css`，`js`等，复杂一些得项目需要`gulp` `grunt` `webpack`等，还得从别的项目中把配置拷贝过来进行修改（配置我记不住。。。），通过这个工具可以省去一些繁琐的，没有技术含量的搭建过程。实现细节，这里就不详细介绍了可以直接去看[源码](https://github.com/zkboys/zk-init)
