---
title: js判断对象是否为空
date: 2016-10-09 11:37:10
category: [前端, JS]
tags: [js]
---
一个工具方法，判断对象是否没有任何属性，即：{}，代码摘取自[jQuery.isEmptyObject()](http://api.jquery.com/jQuery.isEmptyObject/)
```js
function isEmptyObject( obj ) {
	var name;
	for ( name in obj ) {
		return false;
	}
	return true;
}
```  
