---
title: 常用css代码片段
date: 2016-06-14 13:45:36
category: [前端, CSS]
tags: [css]
---
```css
/* 块状元素水平居中 */
.auto{margin-left:auto; margin-right:auto;}
/* 清除浮动*/
.fix{*zoom:1;}
.fix:after{display:table; content:''; clear:both;}
/* 基于display:table-cell的自适应布局 */
.cell{display:table-cell; *display:inline-block; width:2000px; *width:auto;}
/* 双栏自适应cell部分连续英文字符换行 */
.cell2{overflow:hidden; _display:inline-block;}
/* 单行文字溢出虚点显 示*/
.ell{text-overflow:ellipsis; white-space:nowrap; overflow:hidden;}
/* css3过渡动画效果 */
.trans{
    -webkit-transition:all .15s;    
            transition:all .15s;
}
/* 大小不定元素垂直居中 */
.dib_vm{display:inline-block; width:0; height:100%; vertical-align:middle;}
/* 加载中背景图片 - 如果您使用该CSS小库，务必修改此图片地址 */
.loading{background:url(about:blank) no-repeat center;}
/* 无框文本框文本域 */
.bd_none{border:0; outline:none;}
/* 绝对定位隐藏 */
.abs_out{position:absolute; left:-999em; top:-999em;}
.abs_clip{position:absolute; clip:rect(0 0 0 0);}
/* 按钮禁用 */
.disabled{outline:0 none; cursor:default!important; opacity:.4; filer:alpha(opacity=40); -ms-pointer-events:none; pointer-events:none;}
/*inline-block与float等宽列表*/
.inline_box{font-size:1em; letter-spacing:-.25em; font-family:Arial;}
.inline_two, .inline_three, .inline_four, .inline_five, .inline_six, .inline_any{display:inline-block; *display:inline; letter-spacing:0; vertical-align:top; *zoom:1;}
.float_two, .float_three, .float_four, .float_five, .float_six{float:left;}
.inline_two, .float_two{width:50%; *width:49.9%;}
.inline_three, .float_three{width:33.33333%; *width:33.3%;}
.inline_four, .float_four{width:25%; *width:24.9%;}
.inline_five, .float_five{width:20%; *width:19.9%;}
.inline_six, .float_six{width:16.66666%; *width:16.6%;}
.inline_fix{display:inline-block; width:100%; height:0; overflow:hidden;}
```
参考链接：
http://www.cnblogs.com/lyzg/p/5561001.html
