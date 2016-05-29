---
title: 使用IntelliJ系列IDE，导致webpack-dev-server监听文件失效问题
date: 2016-05-29 18:48:12
category: [前端, 构建]
tags: [webpack]
---
在使用 IntelliJ系列IDE（比如WebStorm idea等），开始webpack-dev-server,修改文件并保存，webpack-dev-server并没有反应，由于IntelliJ系列IDE会吧文件修改存在一个临时文件中，并不会改变原始文件，而webpack-dev-server监听的又是原始文件，so...

解决办法：just change a setting
