---
title: js 深克隆
date: 2017-02-15 10:47:25
category: [前端, JS]
tags: [js]
---
设计项目中可以使用如下封装或者使用第三方库的实现，比如[loadsh](https://lodash.com/docs/4.17.4#cloneDeep) 

```js
/**
* javascript 深度克隆函数
*/
function deepClone(obj) {
    var _toString = Object.prototype.toString;

    // null, undefined, non-object, function
    if (!obj || typeof obj !== 'object') {
        return obj;
    }

    // DOM Node
    if (obj.nodeType && 'cloneNode' in obj) {
        return obj.cloneNode(true);
    }

    // Date
    if (_toString.call(obj) === '[object Date]') {
        return new Date(obj.getTime());
    }

    // RegExp
    if (_toString.call(obj) === '[object RegExp]') {
        var flags = [];
        if (obj.global) { flags.push('g'); }
        if (obj.multiline) { flags.push('m'); }
        if (obj.ignoreCase) { flags.push('i'); }

        return new RegExp(obj.source, flags.join(''));
    }

    var result = Array.isArray(obj) ? [] :
        obj.constructor ? new obj.constructor() : {};

    for (var key in obj ) {
        result[key] = deepClone(obj[key]);
    }

    return result;
}

function A() {
    this.a = a;
}

var a = {
    name: 'qiu',
    birth: new Date(),
    pattern: /qiu/gim,
    container: document.body,
    hobbys: ['book', new Date(), /aaa/gim, 111]
};

var c = new A();
var b = deepClone(c);
console.log(c.a === b.a);
console.log(c, b);
```
