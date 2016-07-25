---
title: 关于vue中自定义事件的理解
date: 2016-07-25 12:57:37
category: [JS]
tags: [vue]
---
事件不外乎两部分内容，监听/触发，下面根据这两部分，简单介绍一下vue中的自定义事件。

## 监听
### $on()
- 示例提供得方法，可以通过this.$on(event, callback)直接调用
- 事件可以通过 this.$emit, this.$dispatch 或this.$broadcast触发。
```js
...
ready() {
    this.$on('customer-event', () => {
      ...
    });
  },
...    
```
### $once()
- 示例提供得方法，可以通过this.$once(event, callback)直接调用
- 监听一个自定义事件，但是只触发一次，在第一次触发之后删除监听器。

### v-on:event
当子组件触发了 "customer-event" 事件，父组件的 handleIt 方法将被调用。所有影响父组件状态的代码放到父组件的 handleIt 方法中；子组件只关注触发事件。
```html
<child v-on:customer-event="handleIt"></child>
```

### events
示例提供的方法，在创建实例时 `events` 选项简单地调用 `$on`
```js
events: {
  'customer-event'(msg) {
    // 事件回调内的 `this` 自动绑定到注册它的实例上
    this.messages.push(msg)
  }
}
```

## 触发

### $emit
当前组件内部触发事件，事件不会冒泡到父级，只有当前组件内部才可以捕获到

### $dispatch
派发事件，事件沿着父链冒泡；

### $broadcast
广播事件，事件向下传导给所有的后代。


参考链接：
[http://cn.vuejs.org/api/#实例方法-事件](http://cn.vuejs.org/api/#实例方法-事件)
