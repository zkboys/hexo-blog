---
title: cross-env
date: 2018-02-27 14:13:14
category: [工具]
tags: [cross-env]
---
> 不同平台命令有兼容性问题，可以通过一些第三方包解决

##[rimraf](https://www.npmjs.com/package/rimraf)
> 删除文件、文件夹

## [mkdirp](https://github.com/substack/node-mkdirp)
> 创建文件夹

## [cross-env](https://www.npmjs.com/package/cross-env) 
>不同平台（window linux unix）命令行传递参数有兼容性问题，通过cross-env可以解决各个平台的兼容性问题

### 安装
```
$ yarn add cross-env --dev

或者

$ npm install cross-env --save-dev
```
### 使用

```
// package.jsxon
...
"scripts": {
    "dev": "cross-env NODE_ENV=development node ./builder/dev-server.js",
  },
...
```
`NODE_ENV=development` 常用参数，构建工具以此区分不同的模式，开发模式（development 或 dev）还是生产环境（production 或 pro）；
具体需要什么 参数=值 以项目为准；

