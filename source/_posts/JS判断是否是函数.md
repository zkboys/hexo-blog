---
title: JS判断是否是函数
date: 2017-02-15 11:08:20
category: [前端, JS]
tags: [js]
---
设计项目中可以使用如下封装或者使用第三方库的实现，比如[loadsh](https://lodash.com/docs/4.17.4#isFunction),jQuery等isFunction方法
```js
function isFunction(arg) {
    if (arg) {
        if (typeof (/./) !== 'function') {
            return typeof arg === 'function';
        } else {
            return Object.prototype.toString.call(arg) === '[object Function]';
        }
    }
    return false;
}
console.log(isFunction(function(){}));
```
