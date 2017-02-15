---
title: JS时间监听器
date: 2017-02-15 11:05:51
category: [前端, JS]
tags: [js]
---
一般都使用jQuery 少数情况会 用到原生，可以考虑使用如下封装
```js
function addListener(el, type, listener, useCapture){
  if (window.addEventListener) {
    el.addEventListener(type, listener, useCapture);
    return listener;
  }
  if (window.attachEvent){
    // 标准化this，event，target
    var wrapper = function () {
      var event = window.event;
      event.target = event.srcElement;
      listener.call(el, event);
    };

    el.attachEvent('on' + type, wrapper);
    return wrapper;
  }
}

addListener(document.getElementById('test'), 'click', function(e){
  console.log(e);
});

```
