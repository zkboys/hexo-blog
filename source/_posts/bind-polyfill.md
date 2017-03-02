---
title: bind polyfill
date: 2017-03-02 15:25:16
category: [前端, JS]
tags: [polyfill]
---
老版本浏览器可能不支持bind函数，这里做一个polyfill。
```js
if(!Function.prototype.bind){
    Function.prototype.bind = function(obj){
        var slice = [].slice,
            //bind 函数是可以传参数的。比如：this.click.bind(this,1,2,3)
            args = slice.call(arguments, 1),
            self = this,
            nop = function(){},
            bound = function(){
                return self.apply(this instanceof nop ? this:(obj||{}),
                    args.concat(slice.call(arguments)));
            };
        nop.prototype = self.prototype;
        bound.prototype = new nop();
        return bound;
    };
}
```
