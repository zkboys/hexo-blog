---
title: 自定义webpack loader简化react-router按需加载写法
date: 2016-09-01 17:22:01
category: [前端, 构建]
tags: [webpack]
---
使用react-router时，需要在开始异步获取组件/获取完成/组件是否需要渲染等时刻加入hock（使用发布订阅发送消息），按需加载写法本来就比较繁琐，加上这些hock，更加繁琐了：
```js
{
    path: '/dev/components',
    getComponent: (nextState, cb) => {
        startFetchingComponent();
        require.ensure([], (require) => {
            if (!shouldComponentMount(nextState)) return;
            endFetchingComponent();
            cb(null, connectComponent(require('./sys-component/SysComponent')));
        });
    },
},
```
其中startFetchingComponent shouldComponentMount endFetchingComponent 方法会使用发布订阅发送消息，connectComponent用来链接redux

## 想要的结果
简化写法如下就能实现如上功能：
```js
{
    path: '/dev/components',
    asyncComponent: './sys-component/SysComponent',
},
```

## 自定义routes-loader实现
webpack 自定义loader请参考：[如何开发一个 Webpack Loader](http://www.alloyteam.com/2016/01/webpack-loader-1/)
```js
function getComponentString(componentPath) {
    return "getComponent: (nextState, cb) => {"
        + "startFetchingComponent();"
        + "require.ensure([], (require) => {"
        + "if (!shouldComponentMount(nextState)) return;"
        + "endFetchingComponent();"
        + "cb(null, connectComponent(require('" + componentPath + "')));"
        + "});"
        + "},";
}

module.exports = function (source, other) {
    this.cacheable();
    var routesStrTemp = source;
    var patt = /asyncComponent:[ ]*['"]([^'"]+)['"][,]/gm;
    var isRoutes = false;
    var block = null;
    while ((block = patt.exec(source)) !== null) {
        isRoutes = block[0] && block[1];
        if (isRoutes) {
            routesStrTemp = routesStrTemp.replace(block[0], getComponentString(block[1]));
        }
    }
    if (isRoutes) {
        routesStrTemp = "import connectComponent from 'src/utils/connectComponent.js';\n"
            + "import {startFetchingComponent, endFetchingComponent, shouldComponentMount} from 'src/utils/route-utils';"
            + routesStrTemp;
        this.callback(null, routesStrTemp, other);
    } else {
        this.callback(null, source, other);
    }
};
```
## webpack 配置
由于这是对原routes.js文件的修改，故routes-loader加在preLoaders中,
```js
preLoaders: [
    ...
    {
        test: /routes\.js$/,
        loader: path.join(__dirname, './routes-loader'), // 这里要使用绝对路径
        include: projectRoot,
        exclude: /node_modules/
    }
    ...
],
```
