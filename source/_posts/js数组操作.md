---
title: js数组操作
date: 2016-04-19 13:51:54
category: [前端, JS]
tags: [js]
---
## 数组基本方法：
### concat()

用于链接2个或多个数组，不改变现有数组，返回一个数组。

**语法：arr.concat(arr1, arr2, arr3, ...arrN);**
```javascript
var a1 = [1, 2, 3];
var a2 = [4, 5, 6];
var a3 = [7, 8, 9];

console.log(a1.concat(a2, a3)); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
console.log(a1); // [1, 2, 3]
console.log(a2); // [4, 5, 6]
console.log(a3); // [7, 8, 9]

```

### join()

将数组的所有元素拼接成一个字符串，不改变现有数组，返回一个字符串。

**语法：arr.join([separator]);**

separator: 指定链接各个元素的符号，默认为英文逗号。
```javascript
var arr = ['a', 'b', 'c'];

console.log(arr.join()); // a,b,c
console.log(arr.join('-')); // a-b-c
```

### push()

数组尾部添加1个或者多个元素，改变原有数组，返回改变之后的数组长度。

**语法：arr.push(elem1, elem2, ...elemN)**

如果参数为空，则直接返回数组长度，不对数组有任何操作
```javascript
var arr = ['a', 'b', 'c'];

console.log(arr.push()); // 3
console.log(arr); // ["a", "b", "c"]
console.log(arr.push('d')); // 4
console.log(arr); // ["a", "b", "c", "d"]

console.log(arr.push('e', 'f')); // 6
console.log(arr); // ["a", "b", "c", "d", "e", "f"]
```
### pop()

数组尾部删除1个元素，改变原有数组，返回被删除元素，如果数组为空，返回undefined。

**语法：arr.pop()**

```javascript
var arr = ['a', 'b', 'c'];

console.log(arr.pop()); // c
console.log(arr); // ["a", "b"]

var arr2 = [];
console.log(arr2.pop()); // undefined
console.log(arr2); // []

```

### reverse()

颠倒数组中元素得顺序，改变原有数组，返回颠倒完成之后的数组

**语法：arr.reverse()**

```javascript
var arr = ['a', 'b', 'c'];

var arr2 = arr.reverse();

console.log(arr2); // ["c", "b", "a"]

console.log(arr); // ["c", "b", "a"]
```

### unshift()

数组头部添加1个或多个元素，改变原有数组，返回改变之后的数组长度。

**语法：arr.unshift(elem1, elem2, ...elemN)**

如果参数为空，则直接返回数组长度，不对数组有任何操作
```javascript
var arr = ['a', 'b', 'c'];

console.log(arr.unshift()); // 3
console.log(arr); // ["a", "b", "c"]
console.log(arr.unshift('d')); // 4
console.log(arr); // ["d", "a", "b", "c"]

console.log(arr.unshift('e', 'f')); // 6
console.log(arr); // ["e", "f", "d", "a", "b", "c"]
```
注：unshift和push两个方法非常类似，只不过一个再头部添加，一个在尾部添加。

### shift()

数组头部删除1个元素，改变原有数组，返回被删除元素，如果数组为空，返回undefined。

**语法：arr.shift()**

```javascript
var arr = ['a', 'b', 'c'];

console.log(arr.shift()); // a
console.log(arr); // ["b", "c"]

var arr2 = [];
console.log(arr2.shift()); // undefined
console.log(arr2); // []

```

### sort()

对数组的元素进行排序，改变原有数组，返回排序之后的数组。

**语法：arr.sort([sortby])**

如果参数为空，默认按字母得字符编码顺序排序。

sortby为接受两个参数的函数，返回用于说明这两个参数顺序得数字，比如参数为a，b：

a小于b，即排序之后a在b之前，sortby函数需要返回一个小于0的值；

a等于b，sortby函数需要返回一个等于0的值；

a大于b，即排序之后b在a之前，sortby函数需要返回一个大于0的值；
```javascript
var arr = ['just', 'do', 'it', '!'];

console.log(arr.sort()); // ["!", "do", "it", "just"]
console.log(arr); // ["!", "do", "it", "just"]

var arr2 = [12, 28, 1, 99, 23, 27];

console.log(arr2.sort()); // [1, 12, 23, 27, 28, 99]

console.log(arr2.sort(function(a,b){
  return a-b;
})); // [1, 12, 23, 27, 28, 99]

console.log(arr2.sort(function(a,b){
  return b-a;
})); // [99, 28, 27, 23, 12, 1]

var arr3 = [
  {
    name: '张三',
    age: 22
  },
  {
    name: '李四',
    age: 15
  },
  {
    name: '王五',
    age: 27
  }
];

var arr4 = arr3.sort(function(a, b){
  return a.age-b.age;
});
for(var i = 0;i<arr4.length;i++){
  console.log(arr4[i].name, arr4[i].age);
}
/*
李四 15
张三 22
王五 27
*/
```


### slice()

获取现有数组中指定元素，不改变原有数组，返回一个数组。

**语法：arr.slice(start, end)**

如果start， end 都缺省，返回与原数组相同的一个数组；

如果只传如start，缺省end，返回从start开始至原数组末尾所有元素组成的数组

具体传参方式参考如下例子：

```javascript
var arr = [1, 2, 3, 4, 5, 6];

console.log(arr.slice()); // [1, 2, 3, 4, 5, 6]
console.log(arr.slice(0)); // [1, 2, 3, 4, 5, 6]
console.log(arr.slice(1)); // [2, 3, 4, 5, 6]
console.log(arr.slice(1, 3)); // [2, 3]
console.log(arr.slice(1, -2)); // [2, 3, 4] 5的位置相当于-2, 6的位置相当于-1
console.log(arr.slice(-3, -1)); // [4, 5] 4的位置是-3
console.log(arr.slice(4, 1)); // []
console.log(arr);  // [1, 2, 3, 4, 5, 6]
```

### splice()

插入， 删除， 替换数组元素，改变原有数组，返回删除的所有元素组成的数组。

**语法：arr.splice(start, count, elem1, elem2, ...elemN)**

start：插入或者删除元素得起始位置

count：删除元素得个数

elem1：从start位置开始插入的元素

```javascript
var arr = ['a', 'b', 'c', 'd', 'e', 'f', 'g'];

console.log(arr.splice()); // [] 相当于啥也没做
console.log(arr); // ["a", "b", "c", "d", "e", "f", "g"]
console.log(arr.splice(1)); // ["b", "c", "d", "e", "f", "g"] 从1开始到数组结尾的元素全部删除
console.log(arr); // ["a"]
console.log(arr.splice(1, 2)); // ["b", "c"] 从索引为1开始删除2个元素
console.log(arr); // ["a", "d", "e", "f", "g"]

arr = ['a', 'b', 'c', 'd', 'e', 'f', 'g'];
console.log(arr.splice(1, 0, 'h')); // [] 在1的位置插入h
console.log(arr); // ["a", "h", "b", "c", "d", "e", "f", "g"]

arr = ['a', 'b', 'c', 'd', 'e', 'f', 'g'];
console.log(arr.splice(1, 3, 'h', 'i'));// ["b", "c", "d"]从1的位置开始 删除3个元素，并插入h，i两个元素。
console.log(arr); // ["a", "h", "i", "e", "f", "g"]

```

### toString()

将数组转化为一个字符串，不改变原有数组，返回一个字符串

**语法：arr.toString()**

```javascript
var arr = ['a', 'b', 'c', 'd', 'e', 'f', 'g'];
console.log(arr.toString()); // a,b,c,d,e,f,g
console.log(arr); // ["a", "b", "c", "d", "e", "f", "g"]

```


## ES5 数组的扩展
### forEach()

遍历循环一个数组

**语法：arr.forEach(func[, context])**

func:一个函数，这个函数接受三个参数value, index, array，每次遍历的数组元素，元素对应的索引，原数组。

context：上下文，用来改变func中this的指向。

```javascript
var arr = ['a', 'b', 'c'];
arr.forEach(function(value, index, array){
  console.log(value, index, array);
});
/*
a 0 ["a", "b", "c"]
b 1 ["a", "b", "c"]
c 2 ["a", "b", "c"]
*/

// 只是占位得元素不会被forEach遍历
var arr = ['a', , 'c'];
console.log(arr.length); // 3
arr.forEach(function(value, index, array){
  console.log(value, index, array);
});
/*
a 0 ["a", "b", "c"]
c 2 ["a", "b", "c"]
*/

```

### map()

可以理解为映射，基于原数组映射出一个新数组，不改变原数组，返回一个新数组。
**语法：arr.map(func[， context])**

func:一个函数，此函数接受三个参数：value， index， array，必须要有返回值，所有的返回值会组成一个新数组。

context：上下文，用来改变func中this的指向。

```javascript
var arr = [1, 2, 3, 4, 5];
var arr2 = arr.map(function(value, index, array){
  return value*value;
})
console.log(arr); // [1, 2, 3, 4, 5]
console.log(arr2); // [1, 4, 9, 16, 25]

var arr3 = [
  {
    name: '张三',
    age: 22
  },
  {
    name: '李四',
    age: 15
  },
  {
    name: '王五',
    age: 27
  }
];

console.log(arr3.map(function(v){
  return v.name;
})); // ["张三", "李四", "王五"]
```

### filter()
可以理解为‘过滤’，‘筛选’，不改变原数组，返回筛选之后的新数组。
**语法：arr.filter(func[, context])**

func:一个函数，此函数接受三个参数：value， index， array，返回值如果是true或者转化为true得值，则此次遍历的元素就会被加入返回得新数组中（筛选通过！）

context：上下文，用来改变func中this的指向。

```javascript
var arr = [1, 2, 3, 4, 5];
var arr2 = arr.filter(function(v){
  return v>3;
});
console.log(arr2); // [4, 5]
console.log(arr); // [1, 2, 3, 4, 5]

```
### some()

每次遍历只要有一次返回true，some函数就返回true，所有遍历都返回false，some返回false，不改变原有数组，返回boolean值。

**语法：arr.some(func[, context])**

func:一个函数，此函数接受三个参数：value， index， array

context：上下文，用来改变func中this的指向。

```javascript
var arr = [1, 2, 3, 4, 5];
var result = arr.some(function(value, index, array){
  return value>3;
});
console.log(result); // true 4和5 这两个元素大于3了，所有返回true。
console.log(arr); // [1, 2, 3, 4, 5]
```
### every()

每次遍历只要有一次返回false，every函数就返回false，所有遍历都返回true，every返回true，不改变原有数组，返回boolean值。

**语法：arr.every(func[, context])**

func:一个函数，此函数接受三个参数：value， index， array

context：上下文，用来改变func中this的指向。

与some类似，但是every要求每个元素都满足要求，才返回true，some只要一个元素满足要求，就返回true
```javascript
var arr = [1, 2, 3, 4, 5];
var result = arr.every(function(value, index, array){
  return value>0;
});
console.log(result); // true 所有元素都大于0，所以返回true
console.log(arr); // [1, 2, 3, 4, 5]

```

### indexOf()

查询元素在数组中的索引，跟str.indexOf类似。如果未查到，返回-1，否则返回元素所在数组中的索引。

**语法：arr.indexOf(elem[, start])**

elem：要查找得元素

start：开始位置，如果缺省，从开始位置查找（0）

```javascript
var arr = ['a', 'b', 'c', 'd', 'e', 'f'];
console.log(arr.indexOf('g')); // -1
console.log(arr.indexOf('c')); // 2
console.log(arr.indexOf('d', 5)); // -1
```

### lastIndexOf()

与indexOf类似，只不过是从结尾开始查找，从右向左查找。

**语法：arr.lastIndexOf(elem[, start])**

elem：要查找得元素

start：开始位置，如果缺省，从数组末尾开始查找（arr.length-1）

```javascript
var arr = ['a', 'b', 'c', 'd', 'e', 'f'];
console.log(arr.lastIndexOf('g')); // -1
console.log(arr.lastIndexOf('c')); // 2
console.log(arr.lastIndexOf('d', 5)); // 3
```

### reduce()

### reduceRight()

## ES6 数组的扩展
Array.from()

Array.of()

copyWithin()

find()

findIndex()

fill()

entries()

keys()

values()

includes()

数组的空位

数组推导

## 常用数组算法
