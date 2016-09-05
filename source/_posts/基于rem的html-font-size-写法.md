---
title: 基于rem的html font-size 写法
date: 2016-09-05 11:30:01
category: [前端, CSS]
tags: [CSS]
---
rem是相对于html的font-size的大小单位，在做移动端，不同屏幕下自适应很好用，下面是基于不同分辨率，生成html font-size大小的代码

```less
/*
 * 375屏幕为 20px，以此为基础计算出每一种宽度的字体大小
 * 375以下不变，375以上等比放大
*/

@baseWidth: 375px;
@baseFont: 20px;

html {
  font-size: @baseFont;  //默认当做320px宽度的屏幕来处理
}

@bps: 400px, 414px, 480px; // 支持其他分辨率，在这里追加即可

.loop(@i: 1) when (@i <= length(@bps)) {  //注意less数组是从1开始的
  @bp: extract(@bps, @i);
  @font: @bp/@baseWidth*@baseFont;  
  @media only screen and (min-width: @bp){
    html {
      font-size: @font !important;
    }
  }
  .loop((@i + 1));
};
.loop;
```
转换成css为：
```css
html {
  font-size: 20px;
}
@media only screen and (min-width: 400px) {
  html {
    font-size: 21.33333333px !important;
  }
}
@media only screen and (min-width: 414px) {
  html {
    font-size: 22.08px !important;
  }
}
@media only screen and (min-width: 480px) {
  html {
    font-size: 25.6px !important;
  }
}
```
注：less 转换方法 `sudo npm install less -g` `lessc styles.less`
