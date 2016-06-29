---
title: HTML5本地存储
date: 2016-06-29 18:42:19
category: [前端, JS]
tags: [js]
---

分为localStorage和sessionStorage，一个永久有效，一个session级别的，用法完全相同；每个网站5M，用于存储字符串（只能存字符串）。
## 支持情况
![支持情况](support.png)

## 检测
```js
if(window.localStorage){
     //code here
}else{
     //code here
}
```

## 使用
推荐统一使用setItem getItem  removeItem
### 赋值方法
```js
localStorage.a = 3;//设置a为"3"
localStorage["a"] = "sfsf";//设置a为"sfsf"，覆盖上面的值
localStorage.setItem("b","isaac");//设置b为"isaac"
```

### 取值方法
```js
var a1 = localStorage["a"];//获取a的值
var a2 = localStorage.a;//获取a的值
var b = localStorage.getItem("b");//获取b的值
```       

### 清除方法
```js
localStorage.removeItem("c");//清除c的值
localStorage.clear();//全部清除
```       
### 遍历本地存储
这里会把所有的存储都遍历出来，无论是你用的，还是其他程序用的。key最好有个前缀，不容易重复的前缀，这样能区分开数据到底是什么类型
```js
var storage = window.localStorage; //类数组对象
for(var i = 0; i < storage.length; i++){
     //key(i)获得相应的键，再用getItem()方法获得对应的值
     var key = storage.key(i);
     var value = storage.getItem(key);
 }

```
### 异常处理
异常处理很重要，否则会出现莫名其妙得卡死，还不知道问题出在哪里）
主要是存储已满异常，可以考虑使用LRU（Least Recently Used最近最少使用）

```js
try{
     localStorage.setItem(key, value);
}catch(oException){
     if(oException.name == 'QuotaExceededError'){
          console.log('超出本地存储限额！');
          //如果历史信息不重要了，可清空后再设置
          localStorage.clear();
          localStorage.setItem(key,value);
     }
}
```
### 封装
如下是项目中使用的一个简单封装，storage.js，es6语法。
```js
/**
 *  本地存储封装，项目中其他地方不要直接使用localStorage和sessionStorage，统一使用封装。
 *  简化接口，字符串json转换。
 *  如果本地存储使用比较多，可以考虑封装LRU（Least Recently Used最近最少使用）
 */
export default {
    global: {
        get(key) {
            return window.globalStorage ? window.globalStorage[key] : null;
        },
        set(key, jsonValue) {
            window.globalStorage = window.globalStorage ? window.globalStorage : {};
            window.globalStorage[key] = jsonValue;
        },
        remove(key) {
            if (window.globalStorage) {
                delete window.globalStorage[key];
            }
        },
        removeAll() {
            window.globalStorage = {};
        },
    },
    local: {
        get(key) {
            const strValue = localStorage.getItem(key);
            return JSON.parse(strValue);
        },
        set(key, jsonValue) {
            const strValue = JSON.stringify(jsonValue);
            localStorage.setItem(key, strValue);
        },
        remove(key) {
            localStorage.removeItem(key);
        },
        removeAll() {
            localStorage.clear();
        },
    },
    session: {
        get(key) {
            const strValue = sessionStorage.getItem(key);
            return JSON.parse(strValue);
        },
        set(key, jsonValue) {
            const strValue = JSON.stringify(jsonValue);
            sessionStorage.setItem(key, strValue);
        },
        remove(key) {
            sessionStorage.removeItem(key);
        },
        removeAll() {
            sessionStorage.clear();
        },
    },
};

// 使用
import Storage from './storage.js';
Storage.session.get(key);
Storage.session.set(key, jsonValue);
```

参考链接：
http://www.cnblogs.com/xiaowei0705/archive/2011/04/19/2021372.html
