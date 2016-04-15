---
title: webpack构建，js使用script标签引入
date: 2016-04-15 13:48:10
category: [前端, 构建]
tags: [webpack]
---
使用webpack构建大型项目的时候，如果js库引用过多，彼此之间依赖比较复杂，webpack构建过程非常的慢，而且生成得common.js非常大。整个项目中一些第三方得js库可以不用构建，直接在页面上通过script标签引入即可，只通过webpack打包编译业务代码。

我使用过react react-router ant-design等搭建了一个管理系统，光webpack构建就将近2分钟（而且是电脑配置很牛逼得情况下），打包成的common.js未压缩时2M多，压缩之后还有800k~900K，将react 等一些第三方的js通过script标签直接在页面上引入，降低了单个文件的大小，加快了webpack构建速度，配置如下：
```javascript
output: {
      ...
      'libraryTarget': 'var',
      ...
  },
  externals: {
      'react': 'React',
      'react-dom': 'ReactDOM',
      'antd': 'antd',
      "jquery": "jQuery"
  },
```
页面上通过script引入js：
```html
<script src="react-0.14.6.min.js"></script>
<script src="react-dom-0.14.6.min.js"></script>
<script src="antd-0.12.12.min.js"></script>
<script src="jquery.min.js"></script>
```
文件中的写法不变，依然使用es6的import:
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { Breadcrumb } from 'antd';
import $ from 'jquery'
```
