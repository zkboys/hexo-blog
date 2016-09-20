---
title: JS 正则表达式
date: 2016-09-20 18:21:15
category: [前端, JS]
tags: [js]
---

## JavaScript 权威指南第6版摘录一些表格
![正则表达式中的直接量字符.png](正则表达式中的直接量字符.png)
![正则表达式的字符类.png](正则表达式的字符类.png)
![正则表达式的重复字符语法.png](正则表达式的重复字符语法.png)
![正则表达式的选择、分组和引用字符.png](正则表达式的选择、分组和引用字符.png)
![正则表达式中的锚字符.png](正则表达式中的锚字符.png)
![正则表达式修饰符.png](正则表达式修饰符.png)

## 字符串可以使用正则的四个方法
```js
'abc'.search(/abc/);
'abc'.match(/abc/);
'abc'.split(/b/);
'abc'.replace(/abc/, 'def');
```
## 正则对象RegExp属性和方法
```js
// 五个属性
// source global ignoreCase multiLine lastIndex

// 两个方法
// test
// exec
var pattern = /Java/g;
var text = 'JavaScript is more fun than Java!';
var result;
while((result = pattern.exec(text)) !== null){
  console.log("Matched '" + result[0] + "'" + " at Position " + result.index + "; next search begins at " + pattern.lastIndex);
}
```
