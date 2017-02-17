---
title: Vue2.0 跨组件事件
date: 2017-02-17 23:34:52
category: [前端, JS]
tags: [Vue]
---
组件化经常会涉及到跨组件通信，可以通过发布订阅实现，Vue中可以使用一个空的vue实例座位数据总线，实现组件间通信，不需要使用第三方的发布订阅库。
```js
var bus = new Vue()
// 触发组件 A 中的事件
bus.$emit('id-selected', 1)
// 在组件 B 创建的钩子中监听事件
bus.$on('id-selected', function (id) {
  // ...
})
```
实际项目中可以这样封装一下，搞个mixins：
```js
const eventBus = new Vue();
const mixins = {
    data (){
        return {
            eventBus,
        };
    },
}
Vue.mixin(mixins);

// 各个组件中就可以通过如下方式来使用
this.eventBus.$emit(...);
this.eventBus.$on(...);
```
