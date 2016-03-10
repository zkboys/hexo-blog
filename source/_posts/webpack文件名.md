---
title: webpack文件名相关配置和按需加载
date: 2016-03-10 12:28:12
tags:
---
## output.filename
filename是对应于entry里面生成出来的文件名。比如：
```
{
    entry: {
        "index": "./index.jsx"
    },
    output: {
        filename: "[name].min.js",
        chunkFilename: "[name].min.js"
    }
}
```
生成出来的文件名为index.min.js。
## output.chunkname
chunkname 是未被列在entry中，却又需要被打包出来的文件命名配置，一般在按需加载模块时候，会生成文件，这个文件名就是使用output.chunkname进行配置的．一般配置成：
```
output: {
    filename: "[name].min.js",
    chunkFilename: "[name].[chunkhash:8].min.js"
}
```
非entry，但是需要单独打包出来的文件名配置，添加[chunkhash:8]　每次文件内容改变后，文件名都会变．防止浏览器缓存不更新．

## webpack按需加载写法
```
require.ensure(["modules/demo.jsx"], function(require) {
    var a = require("modules/demo.jsx");
    // ...
}, 'demo');
```
这样除了entry之外会生成的文件demo.asd88sss.min.js(asd88sss我乱写的，webpack会根据文件内容生成[chunkhash:8]).

require.ensure() API的第三个参数是给这个模块命名，否则 chunkFilename: "[name].[chunkhash:8].min.js" 中的 [name] 是一个自动分配的、可读性很差的id(就是一个数字)

## 结合React-Router按需加载写法

```
childRoutes: [
  { path: '/login',
    getComponent: (location, cb) => {
      require.ensure([], (require) => {
        cb(null, require('../components/Login'))
      })
    }
  }
  // ...
]
```
react-router 代码片段 其实就是getComponent函数内部使用了require.ensure()
