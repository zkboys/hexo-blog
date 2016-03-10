---
title: html的viewport meta标签
date: 2016-03-09 18:56:19
category: [前端, HTML]
tags: [html,meta]
---

移动设备上浏览器一般会加如下meta标签，会有更好的显示效果
```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
*注：width=device-width 会导致 iPhone 5 添加到主屏后以 WebApp 全屏模式打开页面时出现黑边 [戳这里](http://bigc.at/ios-webapp-viewport-meta.orz)*


## content 参数：
- width viewport 宽度(数值/device-width)
- height viewport 高度(数值/device-height)
- initial-scale 初始缩放比例
- maximum-scale 最大缩放比例
- minimum-scale 最小缩放比例
- user-scalable 是否允许用户缩放(yes/no)
- minimal-ui iOS 7.1 beta 2 中新增属性，可以在页面加载时最小化上下状态栏。这是一个布尔值，可以直接这样写：
```
<meta name="viewport" content="width=device-width, initial-scale=1, minimal-ui">
```

## 其他
而如果你的网站不是响应式的，请不要使用 initial-scale 或者禁用缩放。
```
<meta name="viewport" content="width=device-width,user-scalable=no">
```
适配 iPhone 6 和 iPhone 6plus 则需要写：
```
<meta name="viewport" content="width=375">
<meta name="viewport" content="width=414">
```
## 不同手机viewport width尺寸

操作系统  | 屏幕尺寸 | viewport width
--------|---------|-------------
android | 4.7~5寸| 360px
IOS | 4.7~5寸（iPhone 6）| 375px
android | 5.5寸 | 400px
IOS | 5.5寸（iPhone 6 plus） | 414px
