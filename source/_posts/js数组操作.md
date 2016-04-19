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
这个函数有些复杂，不知到怎么描述好，直接看例子吧：

**语法：arr.reduce(func[, initialValue])**

func：接受4个参数得函数，previous, current, index, array，之前值，当前值，索引，数组本身。func的返回值，会作为下一次迭代时previous的值。

initialValue：可选，表示初始值，如果指定initialValue，则作为初始时previous的值，如果缺省，数组得第一个元素为previous值，第二个元素为current。

```javascript
var arr = [1, 2, 3, 4, 5];
var sum = arr.reduce(function(previous, current, index, array){
  return previous + current;
});
console.log(sum); // 15

过程展开如下：
// 初始：
previous = initialValue = 1, current = 2;
// 第一次迭代 之后
previous = 1 + 2 = 3, current = 3;//current 向后移动一个元素
// 第二次迭代之后
previous = 3 + 3 = 6, current = 4;
// 第三次迭代之后
previous = 6 + 4 = 10, current = 5;
// 第四次迭代之后
previous = 10 + 5 = 15 ,current = undefined// 没有了，退出，返回15；

```

### reduceRight()
和reduce类似，只不过从数组结尾开始，从右向左迭代。


## ES6 数组的扩展
### Array.from()

`Array.from`方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括ES6新增的数据结构Set和Map）。

下面是一个类似数组的对象，`Array.from`将它转为真正的数组。

```javascript
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};

// ES5的写法
var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']

// ES6的写法
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
```

实际应用中，常见的类似数组的对象是DOM操作返回的NodeList集合，以及函数内部的`arguments`对象。`Array.from`都可以将它们转为真正的数组。

```javascript
// NodeList对象
let ps = document.querySelectorAll('p');
Array.from(ps).forEach(function (p) {
  console.log(p);
});

// arguments对象
function foo() {
  var args = Array.from(arguments);
  // ...
}
```

上面代码中，`querySelectorAll`方法返回的是一个类似数组的对象，只有将这个对象转为真正的数组，才能使用`forEach`方法。

只要是部署了Iterator接口的数据结构，`Array.from`都能将其转为数组。

```javascript
Array.from('hello')
// ['h', 'e', 'l', 'l', 'o']

let namesSet = new Set(['a', 'b'])
Array.from(namesSet) // ['a', 'b']
```

上面代码中，字符串和Set结构都具有Iterator接口，因此可以被`Array.from`转为真正的数组。

如果参数是一个真正的数组，`Array.from`会返回一个一模一样的新数组。

```javascript
Array.from([1, 2, 3])
// [1, 2, 3]
```

值得提醒的是，扩展运算符（`...`）也可以将某些数据结构转为数组。

```javascript
// arguments对象
function foo() {
  var args = [...arguments];
}

// NodeList对象
[...document.querySelectorAll('div')]
```

扩展运算符背后调用的是遍历器接口（`Symbol.iterator`），如果一个对象没有部署这个接口，就无法转换。`Array.from`方法则是还支持类似数组的对象。所谓类似数组的对象，本质特征只有一点，即必须有`length`属性。因此，任何有`length`属性的对象，都可以通过`Array.from`方法转为数组，而此时扩展运算符就无法转换。

```javascript
Array.from({ length: 3 });
// [ undefined, undefined, undefinded ]
```

上面代码中，`Array.from`返回了一个具有三个成员的数组，每个位置的值都是`undefined`。扩展运算符转换不了这个对象。

对于还没有部署该方法的浏览器，可以用`Array.prototype.slice`方法替代。

```javascript
const toArray = (() =>
  Array.from ? Array.from : obj => [].slice.call(obj)
)();
```

`Array.from`还可以接受第二个参数，作用类似于数组的`map`方法，用来对每个元素进行处理，将处理后的值放入返回的数组。

```javascript
Array.from(arrayLike, x => x * x);
// 等同于
Array.from(arrayLike).map(x => x * x);

Array.from([1, 2, 3], (x) => x * x)
// [1, 4, 9]
```

下面的例子是取出一组DOM节点的文本内容。

```javascript
let spans = document.querySelectorAll('span.name');

// map()
let names1 = Array.prototype.map.call(spans, s => s.textContent);

// Array.from()
let names2 = Array.from(spans, s => s.textContent)
```

下面的例子将数组中布尔值为`false`的成员转为`0`。

```javascript
Array.from([1, , 2, , 3], (n) => n || 0)
// [1, 0, 2, 0, 3]
```

另一个例子是返回各种数据的类型。

```javascript
function typesOf () {
  return Array.from(arguments, value => typeof value)
}
typesOf(null, [], NaN)
// ['object', 'object', 'number']
```

如果`map`函数里面用到了`this`关键字，还可以传入`Array.from`的第三个参数，用来绑定`this`。

`Array.from()`可以将各种值转为真正的数组，并且还提供`map`功能。这实际上意味着，只要有一个原始的数据结构，你就可以先对它的值进行处理，然后转成规范的数组结构，进而就可以使用数量众多的数组方法。

```javascript
Array.from({ length: 2 }, () => 'jack')
// ['jack', 'jack']
```

上面代码中，`Array.from`的第一个参数指定了第二个参数运行的次数。这种特性可以让该方法的用法变得非常灵活。

`Array.from()`的另一个应用是，将字符串转为数组，然后返回字符串的长度。因为它能正确处理各种Unicode字符，可以避免JavaScript将大于`\uFFFF`的Unicode字符，算作两个字符的bug。

```javascript
function countSymbols(string) {
  return Array.from(string).length;
}
```

### Array.of()

`Array.of`方法用于将一组值，转换为数组。

```javascript
Array.of(3, 11, 8) // [3,11,8]
Array.of(3) // [3]
Array.of(3).length // 1
```

这个方法的主要目的，是弥补数组构造函数`Array()`的不足。因为参数个数的不同，会导致`Array()`的行为有差异。

```javascript
Array() // []
Array(3) // [, , ,]
Array(3, 11, 8) // [3, 11, 8]
```

上面代码中，`Array`方法没有参数、一个参数、三个参数时，返回结果都不一样。只有当参数个数不少于2个时，`Array()`才会返回由参数组成的新数组。参数个数只有一个时，实际上是指定数组的长度。

`Array.of`基本上可以用来替代`Array()`或`new Array()`，并且不存在由于参数不同而导致的重载。它的行为非常统一。

```javascript
Array.of() // []
Array.of(undefined) // [undefined]
Array.of(1) // [1]
Array.of(1, 2) // [1, 2]
```

`Array.of`总是返回参数值组成的数组。如果没有参数，就返回一个空数组。

`Array.of`方法可以用下面的代码模拟实现。

```javascript
function ArrayOf(){
  return [].slice.call(arguments);
}
```

### 数组实例的copyWithin()

数组实例的`copyWithin`方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组。

```javascript
Array.prototype.copyWithin(target, start = 0, end = this.length)
```

它接受三个参数。

- target（必需）：从该位置开始替换数据。
- start（可选）：从该位置开始读取数据，默认为0。如果为负值，表示倒数。
- end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。

这三个参数都应该是数值，如果不是，会自动转为数值。

```javascript
[1, 2, 3, 4, 5].copyWithin(0, 3)
// [4, 5, 3, 4, 5]
```

上面代码表示将从3号位直到数组结束的成员（4和5），复制到从0号位开始的位置，结果覆盖了原来的1和2。

下面是更多例子。

```javascript
// 将3号位复制到0号位
[1, 2, 3, 4, 5].copyWithin(0, 3, 4)
// [4, 2, 3, 4, 5]

// -2相当于3号位，-1相当于4号位
[1, 2, 3, 4, 5].copyWithin(0, -2, -1)
// [4, 2, 3, 4, 5]

// 将3号位复制到0号位
[].copyWithin.call({length: 5, 3: 1}, 0, 3)
// {0: 1, 3: 1, length: 5}

// 将2号位到数组结束，复制到0号位
var i32a = new Int32Array([1, 2, 3, 4, 5]);
i32a.copyWithin(0, 2);
// Int32Array [3, 4, 5, 4, 5]

// 对于没有部署TypedArray的copyWithin方法的平台
// 需要采用下面的写法
[].copyWithin.call(new Int32Array([1, 2, 3, 4, 5]), 0, 3, 4);
// Int32Array [4, 2, 3, 4, 5]
```

### 数组实例的find()和findIndex()

数组实例的`find`方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为`true`的成员，然后返回该成员。如果没有符合条件的成员，则返回`undefined`。

```javascript
[1, 4, -5, 10].find((n) => n < 0)
// -5
```

上面代码找出数组中第一个小于0的成员。

```javascript
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 10
```

上面代码中，`find`方法的回调函数可以接受三个参数，依次为当前的值、当前的位置和原数组。

数组实例的`findIndex`方法的用法与`find`方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回`-1`。

```javascript
[1, 5, 10, 15].findIndex(function(value, index, arr) {
  return value > 9;
}) // 2
```

这两个方法都可以接受第二个参数，用来绑定回调函数的`this`对象。

另外，这两个方法都可以发现`NaN`，弥补了数组的`IndexOf`方法的不足。

```javascript
[NaN].indexOf(NaN)
// -1

[NaN].findIndex(y => Object.is(NaN, y))
// 0
```

上面代码中，`indexOf`方法无法识别数组的`NaN`成员，但是`findIndex`方法可以借助`Object.is`方法做到。

### 数组实例的fill()

`fill`方法使用给定值，填充一个数组。

```javascript
['a', 'b', 'c'].fill(7)
// [7, 7, 7]

new Array(3).fill(7)
// [7, 7, 7]
```

上面代码表明，`fill`方法用于空数组的初始化非常方便。数组中已有的元素，会被全部抹去。

`fill`方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。

```javascript
['a', 'b', 'c'].fill(7, 1, 2)
// ['a', 7, 'c']
```

上面代码表示，`fill`方法从1号位开始，向原数组填充7，到2号位之前结束。

### 数组实例的entries()，keys()和values()

ES6提供三个新的方法——`entries()`，`keys()`和`values()`——用于遍历数组。它们都返回一个遍历器对象（详见《Iterator》一章），可以用`for...of`循环进行遍历，唯一的区别是`keys()`是对键名的遍历、`values()`是对键值的遍历，`entries()`是对键值对的遍历。

```javascript
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1

for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```

如果不使用`for...of`循环，可以手动调用遍历器对象的`next`方法，进行遍历。

```javascript
let letter = ['a', 'b', 'c'];
let entries = letter.entries();
console.log(entries.next().value); // [0, 'a']
console.log(entries.next().value); // [1, 'b']
console.log(entries.next().value); // [2, 'c']
```

### 数组实例的includes()

`Array.prototype.includes`方法返回一个布尔值，表示某个数组是否包含给定的值，与字符串的`includes`方法类似。该方法属于ES7，但Babel转码器已经支持。

```javascript
[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false
[1, 2, NaN].includes(NaN); // true
```

该方法的第二个参数表示搜索的起始位置，默认为0。如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为-4，但数组长度为3），则会重置为从0开始。

```javascript
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
```

没有该方法之前，我们通常使用数组的`indexOf`方法，检查是否包含某个值。

```javascript
if (arr.indexOf(el) !== -1) {
  // ...
}
```

`indexOf`方法有两个缺点，一是不够语义化，它的含义是找到参数值的第一个出现位置，所以要去比较是否不等于-1，表达起来不够直观。二是，它内部使用严格相当运算符（===）进行判断，这会导致对`NaN`的误判。

```javascript
[NaN].indexOf(NaN)
// -1
```

`includes`使用的是不一样的判断算法，就没有这个问题。

```javascript
[NaN].includes(NaN)
// true
```

下面代码用来检查当前环境是否支持该方法，如果不支持，部署一个简易的替代版本。

```javascript
const contains = (() =>
  Array.prototype.includes
    ? (arr, value) => arr.includes(value)
    : (arr, value) => arr.some(el => el === value)
)();
contains(["foo", "bar"], "baz"); // => false
```

另外，Map和Set数据结构有一个`has`方法，需要注意与`includes`区分。

- Map结构的`has`方法，是用来查找键名的，比如`Map.prototype.has(key)`、`WeakMap.prototype.has(key)`、`Reflect.has(target, propertyKey)`。
- Set结构的`has`方法，是用来查找值的，比如`Set.prototype.has(value)`、`WeakSet.prototype.has(value)`。

### 数组的空位

数组的空位指，数组的某一个位置没有任何值。比如，`Array`构造函数返回的数组都是空位。

```javascript
Array(3) // [, , ,]
```

上面代码中，`Array(3)`返回一个具有3个空位的数组。

注意，空位不是`undefined`，一个位置的值等于`undefined`，依然是有值的。空位是没有任何值，`in`运算符可以说明这一点。

```javascript
0 in [undefined, undefined, undefined] // true
0 in [, , ,] // false
```

上面代码说明，第一个数组的0号位置是有值的，第二个数组的0号位置没有值。

ES5对空位的处理，已经很不一致了，大多数情况下会忽略空位。

- `forEach()`, `filter()`, `every()` 和`some()`都会跳过空位。
- `map()`会跳过空位，但会保留这个值
- `join()`和`toString()`会将空位视为`undefined`，而`undefined`和`null`会被处理成空字符串。

```javascript
// forEach方法
[,'a'].forEach((x,i) => log(i)); // 1

// filter方法
['a',,'b'].filter(x => true) // ['a','b']

// every方法
[,'a'].every(x => x==='a') // true

// some方法
[,'a'].some(x => x !== 'a') // false

// map方法
[,'a'].map(x => 1) // [,1]

// join方法
[,'a',undefined,null].join('#') // "#a##"

// toString方法
[,'a',undefined,null].toString() // ",a,,"
```

ES6则是明确将空位转为`undefined`。

`Array.from`方法会将数组的空位，转为`undefined`，也就是说，这个方法不会忽略空位。

```javascript
Array.from(['a',,'b'])
// [ "a", undefined, "b" ]
```

扩展运算符（`...`）也会将空位转为`undefined`。

```javascript
[...['a',,'b']]
// [ "a", undefined, "b" ]
```

`copyWithin()`会连空位一起拷贝。

```javascript
[,'a','b',,].copyWithin(2,0) // [,"a",,"a"]
```

`fill()`会将空位视为正常的数组位置。

```javascript
new Array(3).fill('a') // ["a","a","a"]
```

`for...of`循环也会遍历空位。

```javascript
let arr = [, ,];
for (let i of arr) {
  console.log(1);
}
// 1
// 1
```

上面代码中，数组`arr`有两个空位，`for...of`并没有忽略它们。如果改成`map`方法遍历，空位是会跳过的。

`entries()`、`keys()`、`values()`、`find()`和`findIndex()`会将空位处理成`undefined`。

```javascript
// entries()
[...[,'a'].entries()] // [[0,undefined], [1,"a"]]

// keys()
[...[,'a'].keys()] // [0,1]

// values()
[...[,'a'].values()] // [undefined,"a"]

// find()
[,'a'].find(x => true) // undefined

// findIndex()
[,'a'].findIndex(x => true) // 0
```

由于空位的处理规则非常不统一，所以建议避免出现空位。

### 数组推导

数组推导（array comprehension）提供简洁写法，允许直接通过现有数组生成新数组。这项功能本来是要放入ES6的，但是TC39委员会想继续完善这项功能，让其支持所有数据结构（内部调用iterator对象），不像现在只支持数组，所以就把它推迟到了ES7。Babel转码器已经支持这个功能。

```javascript
var a1 = [1, 2, 3, 4];
var a2 = [for (i of a1) i * 2];

a2 // [2, 4, 6, 8]
```

上面代码表示，通过`for...of`结构，数组`a2`直接在`a1`的基础上生成。

注意，数组推导中，`for...of`结构总是写在最前面，返回的表达式写在最后面。

`for...of`后面还可以附加`if`语句，用来设定循环的限制条件。

```javascript
var years = [ 1954, 1974, 1990, 2006, 2010, 2014 ];

[for (year of years) if (year > 2000) year];
// [ 2006, 2010, 2014 ]

[for (year of years) if (year > 2000) if(year < 2010) year];
// [ 2006]

[for (year of years) if (year > 2000 && year < 2010) year];
// [ 2006]
```

上面代码表明，`if`语句要写在`for...of`与返回的表达式之间，而且可以多个`if`语句连用。

下面是另一个例子。

```javascript
var customers = [
  {
    name: 'Jack',
    age: 25,
    city: 'New York'
  },
  {
    name: 'Peter',
    age: 30,
    city: 'Seattle'
  }
];

var results = [
  for (c of customers)
    if (c.city == "Seattle")
      { name: c.name, age: c.age }
];
results // { name: "Peter", age: 30 }
```

数组推导可以替代`map`和`filter`方法。

```javascript
[for (i of [1, 2, 3]) i * i];
// 等价于
[1, 2, 3].map(function (i) { return i * i });

[for (i of [1,4,2,3,-8]) if (i < 3) i];
// 等价于
[1,4,2,3,-8].filter(function(i) { return i < 3 });
```

上面代码说明，模拟`map`功能只要单纯的`for...of`循环就行了，模拟`filter`功能除了`for...of`循环，还必须加上`if`语句。

在一个数组推导中，还可以使用多个`for...of`结构，构成多重循环。

```javascript
var a1 = ['x1', 'y1'];
var a2 = ['x2', 'y2'];
var a3 = ['x3', 'y3'];

[for (s of a1) for (w of a2) for (r of a3) console.log(s + w + r)];
// x1x2x3
// x1x2y3
// x1y2x3
// x1y2y3
// y1x2x3
// y1x2y3
// y1y2x3
// y1y2y3
```

上面代码在一个数组推导之中，使用了三个`for...of`结构。

需要注意的是，数组推导的方括号构成了一个单独的作用域，在这个方括号中声明的变量类似于使用`let`语句声明的变量。

由于字符串可以视为数组，因此字符串也可以直接用于数组推导。

```javascript
[for (c of 'abcde') if (/[aeiou]/.test(c)) c].join('') // 'ae'

[for (c of 'abcde') c+'0'].join('') // 'a0b0c0d0e0'
```

上面代码使用了数组推导，对字符串进行处理。

数组推导需要注意的地方是，新数组会立即在内存中生成。这时，如果原数组是一个很大的数组，将会非常耗费内存。

参考链接：

http://www.cnblogs.com/tugenhua0707/p/5052808.html

http://www.zhangxinxu.com/wordpress/2013/04/es5%E6%96%B0%E5%A2%9E%E6%95%B0%E7%BB%84%E6%96%B9%E6%B3%95/

http://es6.ruanyifeng.com/#docs/array
