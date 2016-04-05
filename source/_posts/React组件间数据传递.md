---
title: React组件间数据传递
date: 2016-04-05 12:57:41
category: [前端]
tags: [React]
---
组件间的数据管理，可以使用flux，redux，reflux等方案，如果不使用这些方案，组件间该如何传递数据？本文提供了几个办法。
## 组件关系
组件关系可以分为两种，一种是有层级关系得，即：父子组件；另一种是没有层级关系，即：没有公共的父级组件或者祖先组件。（感觉我在说废话)。

## 父组件给子组件传递数据
父组件可以通过props给子组件传递数据。子组件通过this.props可以获取到父级组件传递过来的数据。

## 子组件给父组件传递数据
父组件通过props，给子组件提供一个方法，方法是用来修改父组件数据，子组件调用方法，可以将子组件得数据传递给父组件;

代码片段如下：
```javascript
state={
  childData:{}
}
render(){
  return <ChildComponent setParentData={(dataFromChild)=>this.setState({childData:dataFromChild})}/>
}
//子组件通过调用 this.props.setParentData(dataFromChild);即可将数据传给父级组件。
```
## 没有层级关系的组件间传递数据
可以使用发布订阅模式，进行数据通信；其实父子关系得组件间也可以使用发布订阅模式。flux，redux等解决方案，本质上其实也是发布订阅模式。
