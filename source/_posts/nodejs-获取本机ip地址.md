---
title: nodejs 获取本机ip地址
date: 2016-12-22 14:45:05
category: [后端, node]
tags: [node]
---
```js
exports = module.exports = function getIPAddress() {
    var interfaces = require('os').networkInterfaces();
    for (var devName in interfaces) {
        var iface = interfaces[devName];
        for (var i = 0; i < iface.length; i++) {
            var alias = iface[i];
            if (alias.family === 'IPv4' && alias.address !== '127.0.0.1' && !alias.internal) {
                return alias.address;
            }
        }
    }
}

```
