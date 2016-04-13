---
title: webpack 监听html文件
date: 2016-04-13 17:34:38
category: [前端, 构建]
tags: [webpack]
---
在使用webpack-dev-server时，js改变，webpack就会重新构建项目，并且浏览器会自动刷新，但是编辑html文件时，webpack-dev-server却毫无反应。

原因由于webpack（webpack-dev-server）只监听有依赖得相关文件，比如html等没有依赖的文件是不会被webpack watch监听的。

既然有依赖关系才会被webpack watch监听，那么就把html文件添加到webpack构建过程中去，就可以监听html文件了。本文介绍一个方法，仅供参考

## 最终效果
- 开发过程中可以监听html文件，编辑html文件，浏览器会自动刷新；
- 最终构建生成的线上文件不能有为了监听html，而加入的html依赖内容。

## 准备
webpack配置文件要能根据命令行参数区分不同的开发模式（runmod）。

为了兼容各个平台命令行参数的写法，这里使用cross-env模块

安装方法：
```
npm install cross-env --save-dev
```
使用方法，在 node 的package.json中定义一个scripts:
```
"scripts" :{
  "dev" : "cross-env runmod=devserver webpack-dev-server --port 8086 --progress --inline"
}
```
终端输入`npm run dev` 即可运行如上命令


创建一个 `watch-html.js`文件：
``` javascript
// RUNMOD 是在webpack.config.js中配置的： new webpack.DefinePlugin({"RUNMOD": JSON.stringify(runmod)}),
if (RUNMOD === 'devserver') {
    require('./index.html');// 这个引入只是让index.html可以被webpack watch 监听
    require('./demo/demo.html');
}

```


## webpack.config.js文件配置
webpack.config.js文件中可以使用 `var runmod = process.env.runmod` 获取到命令行传入得参数（`runmod=devserver`）

通过`new webpack.DefinePlugin({"RUNMOD": JSON.stringify(runmod)})`方式可以把`RUNMOD`参数传给每一个通过webpack构建的js文件。参见`watch-html.js`

将watch-html.js文件加入`entry`:
```javascript
var _entry = {
    //"index": ["./src/home/home.jsx", "./src/home/home-content.jsx"],//会合并成一个index.js
    "index": './index.js',
    "demo": './demo/demo.js'
};
if (runmod === 'devserver') {// 只有devserver模式，才加入监听html文件
    _entry["watch-html"] = './watch-html.js';
}
...
module.exports = {
    ...
    /*
     * 入口文件配置
     * */
    entry: _entry,
    ...
  }
```
将所需要进行监听得文件加入`watch-html.js`文件中就可以实现开发模式（devserver模式）下监听html文件，其他模式（线上 测试 等）不会监听html文件。
