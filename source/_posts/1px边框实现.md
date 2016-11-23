---
title: 1px边框实现
date: 2016-11-22 22:00:19
category: [前端, CSS]
tags: [css]
---
iphone手机，设置border:1px solid #000,实际显示要比一像素要宽，具体原因请自己Google，
通过transform: scale(0.5)可以实现1像素border，具体封装如下：
注意：
- 要显示border的元素需要设置：position:relative或者position:absolute;
- 同时只能设置一个top或者bottom（一个left或者right）
因为top和left是使用：after，left和right使用的是before；
- 这种方式无法设置border-radius;
```less
@borderDefaultWidth: 1px;
@borderDefaultColor: #e8e8e8;

.border-top(@width: @borderDefaultWidth, @color: @borderDefaultColor) {
  &:after {
    top: 0;
    .border-top-bottom-style(@width, @color);
  }
  .media()
}

.border-bottom(@width: @borderDefaultWidth, @color: @borderDefaultColor) {
  &:after {
    bottom: 0;
    .border-top-bottom-style(@width, @color);
  }
  .media()
}

.border-right(@width: @borderDefaultWidth, @color: @borderDefaultColor) {
  &:before {
    right: 0;
    .border-left-right-style(@width, @color);
  }
  .media()
}

.border-left(@width: @borderDefaultWidth, @color: @borderDefaultColor) {
  &:before {
    left: 0;
    .border-left-right-style(@width, @color);
  }
  .media()
}

.border-top-bottom-style(@width, @color) {
  content: "\20";
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  -webkit-transform-origin: 50% 100%;
  transform-origin: 50% 100%;
  height: @width;
  background-color: @color;
}

.border-left-right-style(@width, @color) {
  content: "\20";
  display: block;
  position: absolute;
  top: 0;
  bottom: 0;
  -webkit-transform-origin: 100% 50%;
  transform-origin: 100% 50%;
  width: @width;
  background-color: @color;
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
