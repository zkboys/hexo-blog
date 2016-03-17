---
title: React ES6写法
date: 2016-03-17 13:55:12
category: [前端, JS]
tags: [React]
---
React 最新版本支持ES6的写法,配合上Babel,写起来挺嗨的,总结一下ES6的一些写法:

## React ES6+写法
``` javascript
// 多加一层继承, 可以在baseComponent中做一些文章.
class baseComponent extends React.Component{
    // 构造函数
    constructor(props){
        super(props);
    }
    // ...其他公用代码,方法等封装
}    
//定义类 并继承baseComponent
class App extends baseComponent{
    // 构造函数
    constructor(props){
        super(props);
    }
    // 初始化state,替代原getInitialState, 注意前面没有static
    state = {
        showMenu:false
    };
    // 替代原propTypes 属性,注意前面有static,属于静态方法.
    static propTypes = {
        autoPlay: React.PropTypes.bool.isRequired
    }
    // 默认defaultProps,替代原getDefaultProps方法, 注意前面有static
    static defaultProps = {
        loading:false
    };
    // 事件的写法,这里要使用箭头函数,箭头函数不会改变this的指向,否则函数内,this指的就不是当前对象了
    // React.CreatClass方式React会自动绑定this,ES6写法不会.详见下一小节说明.
    handleClick = (e)=>{
        this.setState();//这里的this指的还是App
    };
    componentDidMount() {
        // React内置的周期函数,这里要显示的调用父类的相应函数,
        // 否则一旦父类中有封装,子类会把父类相应函数覆盖掉,不会执行父类的函数.
        // 需要判断一下...父类一旦没有实现componentDidMount,这里直接调用就会报错,
        // 最好是父类都实现相应的方法,子类就不用判断了.
        if (super.componentDidMount) {
            super.componentDidMount();
        }
        // do something yourself...
    }
}
```
## 官方的一个例子:
```javascript
export class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: props.initialCount};
  }
  tick() {
    this.setState({count: this.state.count + 1});
  }
  render() {
    return (
      <div onClick={this.tick.bind(this)}>
        Clicks: {this.state.count}
      </div>
    );
  }
}
Counter.propTypes = { initialCount: React.PropTypes.number };
Counter.defaultProps = { initialCount: 0 };
```
## React ES6 事件绑定
官方原话:

> Autobinding: When creating callbacks in JavaScript, you usually need to explicitly bind a method to its instance such that the value of this is correct. With React, every method is automatically bound to its component instance. React caches the bound method such that it's extremely CPU and memory efficient. It's also less typing!

新的ES6写法如果要实现this还指向当前对象,有三种写法:个人感觉箭头函数写法最优雅.
```javascript
第一种:this._handleClick.bind(this)

_handleClick(e) {
    console.log(this);
}
render() {
    return (
        <div>
            <h1 onClick={this._handleClick.bind(this)}>点击</h1>
        </div>
    );
}
第二种:this._handleClick = this._handleClick.bind(this)

constructor(props) {
    super(props);
    this._handleClick = this._handleClick.bind(this)
}
_handleClick(e) {
    console.log(this);
}
render() {
    return (
        <div>
            <h1 onClick={this._handleClick}>点击</h1>
        </div>
    );
}
第三种:_handleClick = (e) => {}

_handleClick = (e) => {
    // 使用箭头函数(arrow function)
    console.log(this);
}
render() {
    return (
        <div>
            <h1 onClick={this._handleClick}>点击</h1>
        </div>
    );
}

```

## React ES6 写法,做封装一些待解决的问题
- 多层继承,props state等属性如何继承?
- 一些周期函数子类如何自动调用?而不是super.componentDidMount()这种显示调用
