---
title: CSS Secrets阅读笔记
date: 2016-04-27 15:36:43
category: [前端, CSS]
tags: [css]
toc: true
---
<style>
  .demo-box{
    position:relative;
    width:300px;
    height:300px;
    background: #f06;
    background: linear-gradient(45deg, #f06, yellow);
  }
  .inner-box{
    position:absolute;
    left:50%;
    top:50%;
    transform:translate(-50%, -50%);
    width:200px;
    height:200px;  
  }
</style>

## 透明边框
```css
div{
  border: 10px solid hsla(0,0%,100%,.5);
  background: white;
  background-clip: padding-box;
}
```
主要属性：
- 边框颜色使用hsla或者rgba
- background-clip设置为padding-box;即背景为padding+content

background-clip三个值：
- border-box	背景被裁剪到边框盒。
- padding-box	背景被裁剪到内边距框。
- content-box	背景被裁剪到内容框。

效果如下：
<style>
.translucent-borders{
  border:10px solid hsla(0,0%,100%,.5);
  background:white;
  background-clip:padding-box;
}
</style>

<div class="demo-box">
  <div class="translucent-borders inner-box"></div>
</div>

官方示例：http://play.csssecrets.io/translucent-borders

## 多重边框

### box-shadow 方案
box-shadow语法：

`box-shadow: h-shadow v-shadow blur spread color inset;`

值|描述
--|----
h-shadow|	必需。水平阴影的位置。允许负值。
v-shadow|	必需。垂直阴影的位置。允许负值。
blur|	可选。模糊距离。
spread|	可选。阴影的尺寸。
color|	可选。阴影的颜色。请参阅 CSS 颜色值。
inset|	可选。将外部阴影 (outset) 改为内部阴影。

```css
div{
  background: yellowgreen;
  box-shadow: 0 0 0 10px #655;
}
```
效果如下：
<style>
  .box-shadow-one-borders{
    background: yellowgreen;
    box-shadow: 0 0 0 10px #655;
  }
</style>

<div class="demo-box">
  <div class="box-shadow-one-borders inner-box"></div>
</div>

两个边框：

```css
div{
  background: yellowgreen;
  box-shadow: 0 0 0 10px #655, 0 0 0 15px deeppink;
}
```

<style>
  .box-shadow-two-borders{
    background: yellowgreen;
    box-shadow: 0 0 0 10px #655, 0 0 0 15px deeppink;
  }
</style>

<div class="demo-box">
  <div class="box-shadow-two-borders inner-box"></div>
</div>

三个边框：
```css
div{
  background: yellowgreen;
  box-shadow: 0 0 0 10px #655,
  0 0 0 15px deeppink,
  0 0 0 20px #632;
}
```
<style>
  .box-shadow-three-borders{
    background: yellowgreen;
    box-shadow: 0 0 0 10px #655,
    0 0 0 15px deeppink,
    0 0 0 20px #632;
    border-radius:5px;
    border:5px dashed #000;
  }
</style>

<div class="demo-box">
  <div class="box-shadow-three-borders inner-box"></div>
</div>

几点说明：

- shadows会忽略box-sizing属性，阴影是加在盒子之外的，可以使用 box-shadow 的 inset 属性解决这个问题。
- shadows会忽略hover click等鼠标事件，同样可以使用inset属性解决，如果有内容，可以使用padding属性，把shadows的空间留出来。
- 不支持dashed边框


官方示例：http://play.csssecrets.io/multiple-borders

### outline 方案

```css
div{
  background: yellowgreen;
  border: 10px solid #655;
  outline: 15px solid deeppink;
}
```
效果如下：

<style>
  .out-line-borders{
    background: yellowgreen;
    border: 5px dashed #655;
    outline: 15px solid deeppink;
  }
</style>

<div class="demo-box">
  <div class="out-line-borders inner-box"></div>
</div>

## 背景位置右下角

```css
方案一
div {
	background: url(http://csssecrets.io/images/code-pirate.svg)
	            no-repeat bottom right #58a;
	background-position: right 20px bottom 10px;
}
方案二
div {
	background: url(http://csssecrets.io/images/code-pirate.svg)
	            no-repeat bottom right #58a;
	background-origin: content-box;
}
方案三
div {
	background: url(http://csssecrets.io/images/code-pirate.svg)
	            no-repeat bottom right #58a;
	background-position: calc(100% - 20px) calc(100% - 10px);
}
```

## 内圆角
```css
div {
	outline: .6em solid #655;
	box-shadow: 0 0 0 .4em #655; /* todo calculate max of this */
}
```

## 条纹背景

```css
div{
  background: #58a;
  background-image: repeating-linear-gradient(30deg,
              hsla(0,0%,100%,.1), hsla(0,0%,100%,.1) 15px,
              transparent 0, transparent 30px);
}
```
## 随机条纹背景
```css
div{
  background: hsl(20, 40%, 90%);
  background-image:
  	linear-gradient(90deg, #fb3 11px, transparent 0),
  	linear-gradient(90deg, #ab4 23px, transparent 0),
  	linear-gradient(90deg, #655 23px, transparent 0);
  background-size: 83px 100%, 61px 100%, 41px 100%;
}
```
各种背景：http://lea.verou.me/css3patterns/ http://bennettfeely.com/gradients/

各种按钮：http://simurai.com/archive/buttons/

## 容器倾斜文字不倾斜
```css
方案一
.button { transform: skewX(45deg); }
.button > div { transform: skewX(-45deg); }

.button {
	display: inline-block;
	padding: .5em 1em;
	border: 0; margin: .5em;
	background: #58a;
	color: white;
	text-transform: uppercase;
	text-decoration: none;
	font: bold 200%/1 sans-serif;
}
方案二
.button {
	position: relative;
	display: inline-block;
	padding: .5em 1em;
	border: 0; margin: .5em;
	background: transparent;
	color: white;
	text-transform: uppercase;
	text-decoration: none;
	font: bold 200%/1 sans-serif;
}

.button::before {
	content: ''; /* To generate the box */
	position: absolute;
	top: 0; right: 0; bottom: 0; left: 0;
	z-index: -1;
	background: #58a;
	transform: skew(45deg);
}
```

## 菱形图片
```css
方案一
.diamond {
	width: 250px;
	height: 250px;
	transform: rotate(45deg);
	overflow: hidden;
	margin: 100px;
}

.diamond img {
	max-width: 100%;
	transform: rotate(-45deg) scale(1.42);
	z-index: -1;
	position: relative;
}
方案二
img {
	max-width: 250px;
	margin: 20px;
	-webkit-clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);
	clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);
	transition: 1s;
}

img:hover {
	-webkit-clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
	clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
}
```
## 单边阴影
```css
div {
	width: 1.6in;
	height: 1in;
	background: #fb3;
	box-shadow: 0 5px 4px -4px black;
}
```
