---
title: JS判断是否是数组
date: 2017-02-15 10:55:07
category: [前端, JS]
tags: [js]
---
设计项目中可以使用如下封装或者使用第三方库的实现，比如[loadsh](https://lodash.com/docs/4.17.4#isArray),jQuery等isArray方法

```js
function isArray(arg) {
  if(Array.isArray){
  	return Array.isArray(arg);
  }
  if (typeof arg === 'object') {
    return Object.prototype.toString.call(arg) === '[object Array]';
  }
  return false;
}
```
