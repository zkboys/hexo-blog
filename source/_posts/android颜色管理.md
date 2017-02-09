---
title: android颜色管理
date: 2017-01-09 14:05:41
category: [android]
tags: [color]
---
优秀的app设计，一般只有几种颜色，各个组件的颜色都是统一的，比如统一的字体颜色，统一的背景颜色，统一的border等，如果设计良好，可以基于所有的设计图，整理出android项目所需要color。
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- 主色调 -->
    <color name="colorPrimary">#f65037</color>
    <!-- 主色调深色 -->
    <color name="colorPrimaryDark">#d34202</color>
    <!-- 输入框获得焦点、单复选框选中、按钮激活颜色 -->
    <color name="colorAccent">#ff0000</color>
    
    <color name="white">#ffffff</color>
    <color name="textColorPrimary">#eeeeee</color>
    <color name="textColorPrimaryDark">#666666</color>
    <color name="windowBackground">#ffffff</color>
    <color name="navigationBarColor">#000000</color>
</resources>

```
