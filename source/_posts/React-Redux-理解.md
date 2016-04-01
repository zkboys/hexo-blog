---
title: React Redux 理解
date: 2016-04-01 11:58:35
category: [前端]
tags: [Redux]
---

初步对Redux的理解，进行一下总结

## 组成部分

### views
组件可以分为两类，component-views controller-views

#### components-views
这个名字是我自己起的，这类组件职责如下：
- 接受父组件（controller-views）的props做展示；
- 调用父组件的方法（通过props传递的），改变数据，一般组件中的事件（比如点击事件），通过pros调用父组件的方法。

#### controller-views
顾名思义，这个view有控制器的功能，主要的作用如下：
- 包含组装其他组件（component-views），通过props为其他组件提供数据；
- 通过props.dispatch调用actions中的方法，处理业务逻辑；
- 通过props为子组件提供方法,供子组件调用。
- 需要通过react-redux connect方法进行包装，将state转换成props。

### actions
为controller-vers提供语义化API，actions中的方法一般只是单纯的返回一个action对象，action约定有个type属性，用来让reducers区分什么样的操作。

### reducers
一些纯函数，接受两个参数，原state数据和action，返回处理好的state，函数中药注意，不要直接改变形参的state，通过assign方法，重新创建一个state，然后返回新建并处理过的state。

## 官方文档
[英文文档](http://redux.js.org/)

[中文文档](http://camsong.github.io/redux-in-chinese/index.html)
