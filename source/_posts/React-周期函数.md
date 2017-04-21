---
title: React 周期函数
date: 2016-05-27 10:45:07
category: [前端, JS]
tags: [React]
---
对于React相关开发，理解React提供得几个周期函数尤为重要，这里简单总结一下，更多内容移步参考链接

## React生命周期图
![React生命周期图](React生命周期.png)

## 周期函数说明

生命周期函数|被调用次数|能否使用setState()|说明
-----|---|----
componentWillMount|1|是|首次渲染前的一些初始化操作，如果涉及到渲染之后的DOM操作，在componentDidMount进行。
render|>=1|否|由于调用比较频繁，尽量少写逻辑，除了获取state，props属性之外的一些变量声明不要在这里做，大块的业务逻辑封装成方法，提出render，保持render清晰简洁。
componentDidMount|1|是|尽量不要在此方法中使用setState，初始化setState操作请在componentWillMount做。
componentWillReceiveProps(object nextProps)|>=0|是|提供了接受新的props之后操作state得机会
shouldComponentUpdate(object nextProps, object nextState)|>=0|否|返回false render不会执行，可以通过此方法优化性能。
componentWillUpdate(object nextProps, object nextState)|>=0|否|
componentDidUpdate(object prevProps, object prevState)|>=0|否|
componentWillUnmount|1|否|

参考链接：
http://www.open-open.com/lib/view/open1446022707992.html

http://reactjs.cn/react/docs/component-specs.html
