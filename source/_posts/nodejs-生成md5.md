---
title: nodejs 生成md5
date: 2017-02-09 18:51:52
category: [后端, node]
tags: [node]
---
```js
const crypto = require('crypto');

function md5(str) {
    const md5sum = crypto.createHash('md5');
    md5sum.update(str);
    str = md5sum.digest('hex');
    return str;
}
```
