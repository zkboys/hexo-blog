---
title: es6 Mixin模式的实现
date: 2016-08-24 16:27:42
category: [前端, JS]
tags: [js]
---
可以用来实现多继承，具体实现如下：
```javascript
function mix(...mixins) {
  class Mix {}

  for (let mixin of mixins) {
    copyProperties(Mix, mixin);
    copyProperties(Mix.prototype, mixin.prototype);
  }

  return Mix;
}

function copyProperties(target, source) {
  for (let key of Reflect.ownKeys(source)) {
    if ( key !== "constructor"
      && key !== "prototype"
      && key !== "name"
    ) {
      let desc = Object.getOwnPropertyDescriptor(source, key);
      Object.defineProperty(target, key, desc);
    }
  }
}
```
上面代码的mix函数，可以将多个对象合成为一个类。使用的时候，只要继承这个类即可。
```javascript
class DistributedEdit extends mix(Loggable, Serializable) {
  // ...
}
```

参考链接：
http://es6.ruanyifeng.com/#docs/class#Mixin模式的实现
