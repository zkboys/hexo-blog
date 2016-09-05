---
title: js一些工具方法
date: 2016-09-05 10:03:44
category: [前端, JS]
tags: [js]
toc: true
---
平时用到的一些小方法，整理起来备用

## 数组乱序
```js
var arr = [0, 1, 2, 3, 4, 5, 6];
arr.sort(function () {
    return 0.5 - Math.random();
})
console.log(arr);
```

## 随机数
```js
/**
 * 获取 min～max之间的一个随机整数
 * @param min
 * @param max
 * @returns {*}
 */
function getRandomNum(min, max) {
    var range = max - min;
    var rand = Math.random();
    return (min + Math.round(rand * range));
}
```
## 日期格式化扩展
```js
/**
 * 日期格式化函数
 * 年：y，1-4个占位符
 * 月：M，日：d，时：h，分：m，秒：s，季度：q， 1-2 个占位符
 * 毫秒：S，1个占位符
 * 例：
 * (new Date()).format('yyyy-MM-dd hh:mm:ss.S') ---> 2016-09-05 10:18:32.976
 * (new Date()).format('yyyy-M-d h:m:s.S')      ---> 2016-9-5 10:18:32.976
 * @param date
 * @param format
 * @returns {*}
 */
function dateFormat(date, format) {
    var symbolMap = {
        "M+": date.getMonth() + 1, //月
        "d+": date.getDate(), //日
        "h+": date.getHours(), //时
        "m+": date.getMinutes(), //分
        "s+": date.getSeconds(), //秒
        "q+": Math.floor((date.getMonth() + 3) / 3), //季度
        "S": date.getMilliseconds() //毫秒
    };
    if (/(y+)/.test(format)) {
        format = format.replace(RegExp.$1, (date.getFullYear() + "").substr(4 - RegExp.$1.length));
    }
    for (var k in symbolMap) {
        if (new RegExp("(" + k + ")").test(format)) {
            format = format.replace(RegExp.$1, (RegExp.$1.length == 1) ? (symbolMap[k]) : (("00" + symbolMap[k]).substr(("" + symbolMap[k]).length)));
        }
    }
    return format;
}

/**
 * 扩展Date，添加格式化功能
 * 年：y，1-4个占位符
 * 月：M，日：d，时：h，分：m，秒：s，季度：q， 1-2 个占位符
 * 毫秒：S，1个占位符
 * 例：
 * (new Date()).format('yyyy-MM-dd hh:mm:ss.S') ---> 2016-09-05 10:18:32.976
 * (new Date()).format('yyyy-M-d h:m:s.S')      ---> 2016-9-5 10:18:32.976
 * @param format
 * @returns {*}
 */
Date.prototype.format = function (format) {
    var symbolMap = {
        "M+": this.getMonth() + 1, //月
        "d+": this.getDate(), //日
        "h+": this.getHours(), //时
        "m+": this.getMinutes(), //分
        "s+": this.getSeconds(), //秒
        "q+": Math.floor((this.getMonth() + 3) / 3), //季度
        "S": this.getMilliseconds() //毫秒
    };
    if (/(y+)/.test(format)) {
        format = format.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
    }
    for (var k in symbolMap) {
        if (new RegExp("(" + k + ")").test(format)) {
            format = format.replace(RegExp.$1, (RegExp.$1.length == 1) ? (symbolMap[k]) : (("00" + symbolMap[k]).substr(("" + symbolMap[k]).length)));
        }
    }
    return format;
};
```

## 根据给定时间，获取给定时间当前周，前一周，后一周的所有日期

```js
/**
 * 根据给定时间，获取给定时间当前周，前一周，后一周的所有日期
 * @param date
 * @returns {{activeDates: Array, prevDates: Array, nextDates: Array}}
 */
function getWeekDateRange(date) {
    var activeDates = [];
    var prevDates = [];
    var nextDates = [];
    var nowTime = date.getTime();
    var day = date.getDay();
    var oneDayLong = 24 * 60 * 60 * 1000;

    for (var i = -7; i < 14; i++) {
        var dateTiem = nowTime + (i - day) * oneDayLong;
        var d = new Date(dateTiem);
        if (i < 0) {
            prevDates.push(d);
        } else if (i < 7) {
            activeDates.push(d);
        } else {
            nextDates.push(d);
        }

    }

    return {
        activeDates: activeDates,
        prevDates: prevDates,
        nextDates: nextDates,
    }
}
```

## 去除字符串前后，左侧，右侧空格
```js
var testStr = '   aaa bbb   ';
// 去掉前后空格
var str = testStr.replace(/(^\s*)|(\s*$)/g, "");

// 去掉左侧空格
var str = testStr.replace(/(^\s*)/g, ""); 

// 去掉右侧空格
var str = testStr.replace(/(\s*$)/g, "");

// 扩展string对象
String.prototype.trim = function() {  
    return this.replace(/(^\s*)|(\s*$)/g, "");  
}  

String.prototype.leftTrim = function() {  
    return this.replace(/(^\s*)/g, "");  
}
  
String.prototype.rightTrim = function() {  
    return this.replace(/(\s*$)/g, "");  
}
```
