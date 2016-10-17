---
title: 关于React ref的使用
date: 2016-08-05 14:00:06
category: [前端, JS]
tags: [React]
---
React应用中，有时需要操作真实得dom节点，比如使用一些第三方，非React插件的时候，需要直接操作dom，React中，可以使用ref获取;
``` js
componentDidMount(){
  const myInput = this.refs.myInput;
}

render(){
  return (
    <div>
      <input ref="myInput"/>
    </div>
  )
}
```
还可以这样写：
``` js
componentDidMount(){
  const myInput = this.myInput;
}

render(){
  return (
    <div>
      <input ref={(view) => this.myInput = view}/>
    </div>
  )
}
```
组件嵌套得时候有个坑：父组件只能获取直接子节点的ref
```js
componentDidMount(){
  // 这里是无法获取到的，由于input得直接父组件是SomeComponent,这时input的ref并未执行
  // 可以在SomeComponent 的 componentDidMount中获取到myInput
  const myInput = this.myInput;
}

render(){
  return (
    <SomeComponent>
      <input ref={(view) => this.myInput = view}/>
    </SomeComponent>
  )
}
```
这个怎么破？组件化，将dom操作封装成一个独立的组件，比如图表（chart），可以把图表单独封装成组件，其他组件调用即可，即可避免组件嵌套ref无法获取的问题，又符合组件化规范，提高复用。
