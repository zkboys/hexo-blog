---
title: 1px边框实现
date: 2016-11-22 22:00:19
category: [前端, CSS]
tags: [css]
---
iphone手机，设置border:1px solid #000,实际显示要比一像素要宽，具体原因请自己Google，
通过transform: scale(0.5)可以实现1像素border，具体封装如下：
注意：要显示border的元素需要设置：position:relative或者position:absolute;同时只能设置一个top或者bottom（一个left或者right）
因为top和left是使用：after，left和right使用的是before；而且这种方式无法设置border-radius
```less
@defaultWidth: 1px;
@defaultColor: #e8e8e8;

.border-top(@width: @defaultWidth, @color: @defaultColor) {
  &:after {
    top: 0;
    width: 100%;
    .border-style(@width, @color);
  }
  .media()
}

.border-bottom(@width: @defaultWidth, @color: @defaultColor) {
  &:after {
    bottom: 0;
    width: 100%;
    .border-style(@width, @color);
  }
  .media()
}

.border-right(@width: @defaultWidth, @color: @defaultColor) {
  &:before {
    right: 0;
    height: 100%;
    .border-style(@width, @color);
  }
  .media()
}

.border-left(@width: @defaultWidth, @color: @defaultColor) {
  &:before {
    left: 0;
    height: 100%;
    .border-style(@width, @color);
  }
  .media()
}

.border-style(@width, @color) {
  content: "\20";
  display: block;
  position: absolute;
  height: @width;
  background-color: @color;
  -webkit-transform-origin: 50% 100%;
  transform-origin: 50% 100%;
}

.media() {
  @media only screen and (-webkit-min-device-pixel-ratio: 2) {
    &:after {
      -webkit-transform: scaleY(0.5);
      transform: scaleY(0.5);
    }
  }

  @media only screen and (-webkit-min-device-pixel-ratio: 3) {
    &:after {
      -webkit-transform: scaleY(0.33333);
      transform: scaleY(0.33333);
    }
  }

  @media only screen and (-webkit-min-device-pixel-ratio: 4) {
    &:after {
      -webkit-transform: scaleY(0.25);
      transform: scaleY(0.25);
    }
  }
}
```
使用方法：
```less
@import '../path-to/mixins.less';
div{
  display: relative;
  .border-top();
  .border-left();
}
```
