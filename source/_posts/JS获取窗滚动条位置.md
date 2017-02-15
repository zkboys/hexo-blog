---
title: JS获取窗滚动条位置
date: 2017-02-15 11:25:15
category: [前端, JS]
tags: [js]
---
如果项目中使用jQuery，请使用jQuery相关方法
```js
/**
 * 获取指定window中滚动条的偏移量，如未指定则获取当前window
 * 滚动条偏移量
 *
 * @param {window} w 需要获取滚动条偏移量的窗口
 * @return {Object} obj.x为水平滚动条偏移量,obj.y为竖直滚动条偏移量
 */
function getScrollOffset(w) {
    w =  w || window;
    // 如果是标准浏览器
    if (w.pageXOffset != null) {
        return {
            x: w.pageXOffset,
            y: w.pageYOffset
        };
    }

    // 老版本IE，根据兼容性不同访问不同元素
    var d = w.document;
    if (d.compatMode === 'CSS1Compat') {
        return {
            x: d.documentElement.scrollLeft,
            y: d.documentElement.scrollTop
        }
    }

    return {
        x: d.body.scrollLeft,
        y: d.body.scrollTop
    };
}
console.log(getScrollOffset());
```
