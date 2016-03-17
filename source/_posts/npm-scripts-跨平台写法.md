---
title: npm scripts 跨平台写法
date: 2016-03-17 14:20:43
category: [前端, 构建]
tags: [npm]
---
 Unix 或者 Windows 的命令行脚本写法有些不同,在不精通这些脚本命令的情况下,可以通过一些工具达到跨平台,使用起来也非常简单.

一个package.json文件实例：源码[戳这里](https://github.com/zkboys/npm-scripts)
```json
{
  "devDependencies": {
    "cross-env": "^1.0.7",
    "mkdirp": "^0.5.1",
    "ncp": "^2.0.0",
    "rimraf": "^2.5.0"
  },
  "scripts": {
    "my": "rimraf my && mkdirp my && ncp build my && cross-env MOD=pro node my.js"
  }
}
```
相应的模块官网:

[删除目录 rimraf](https://www.npmjs.com/package/rimraf)

[创建目录 mkdirp](https://www.npmjs.com/package/mkdirp)

[传递参数 cross-env](https://www.npmjs.com/package/cross-env)

[复制 ncp](https://www.npmjs.com/package/ncp)
