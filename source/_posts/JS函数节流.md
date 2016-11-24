---
title: JS函数节流/截流
date: 2016-03-14 15:44:57
category: [前端, JS]
tags: [js]
---
平时作网页的时候，会给window添加resize，scroll事件，这些事件触发频率比较高，如果事件实现比较复杂，性能较低，可以使用节流/截流方式

*也不知道谁起的名，一个叫节流，一个叫截流*
## 节流
每间隔一个固定的时间调用一次函数，以$(window).resize()为列：
```javascript
$(function() {
    var timer = 0;
    $(window).resize(function() {
        if (!timer) {
            timer = setTimeout(function() {
                //do something...
                timer = 0;
            }, 250)
        }
    }).trigger('resize');//页面初始化的时候立即调用一次
})
```
节流的一个封装
```js
const throttle = function (action, delay) {
    let timeout = null
    let lastRun = 0
    return function () {
        if (timeout) {
            return
        }
        let elapsed = Date.now() - lastRun
        let context = this
        let args = arguments
        let runCallback = function () {
                lastRun = Date.now()
                timeout = false
                action.apply(context, args)
            }
        if (elapsed >= delay) {
            runCallback()
        }
        else {
            timeout = setTimeout(runCallback, delay)
        }
    }
}
$(window).resize(throttle(() => {
  console.log('我会100ms被调用一次');
}, 100));
```

## 截流
实现一个搜索功能，用户输入停止300后触发一次搜索事件。
```javascript
var searchTimeout,
    searchDelay = 300;
$('#search').on('keyup', function (event) {
    clearTimeout(searchTimeout);
    searchTimeout = setTimeout(function () {
        $ajaxForm.triggerHandler('submit');
    }, searchDelay);
});
```
