---
title: css选择器
date: 2016-03-11 10:01:16
category: [前端,CSS]
tags: [css]
---

## CSS常用选择器
闲来无事，复习一下。

选择器|例子|描述|CSS版本
-----|---|----|---
.class|.active|类选择器|1
#id|#wrap|id选择器|1
*|*|通配符，选择所有元素|2
element|p|标签选择器|1
element,element|div,p|逗号选择符，一次性选择多个元素|1
element element|div p|空格选择符，选取所有后代元素|1
element>element|div>p|大于号选择符，选取直接子节点|2
element+element|div+p|加号选择符，紧接着之后的第一个兄弟元素（中间不能有其他元素），直接下一个。|2
element~element|div~p|所有之后的兄弟元素，非兄弟元素不会选中|3
[attr]|div[title]|含有title属性的div元素|2
[attr=value]|div[title=good]|选择title属性为good的div元素|2
[attr~=value]|div[title~=good]|title属相包含good **单词** 的div元素，比如title='good boy!'可以，但是title='goodboy'不可以|2
[attr竖线=value]|div[title竖线=go]|title属性以go开头的所有div元素，还不算是以某个xx开头，这个选择符只有以下几种情况可以：title='go' title='go-' title='go-od' title='go-od boy!',**需要连字符**,这个选择器是不是为lang属性发明的？|2
[attr^=value]|a[src^="https"]|开头：选择其 src 属性值以 "https" 开头的所有a元素|3
[attr$=value]|a[src$=".pdf"]|结尾：选择其 src 属性以 ".pdf" 结尾的所有a元素|3
[attr*=value]|a[src*="abc"]|包含：选择其 src 属性中包含 "abc" 子串的所有a元素|3
:link|a:link|选择所有未被访问的链接|1
:visited|a:visited|选择所有已被访问的链接|1
:active|a:active|选择活动链接|1
:hover|a:hover|选择鼠标指针位于其上的链接|1
:focus|input:focus|选择获得焦点的 input 元素|2
:first-letter|p:first-letter|选择每个 p 元素的首字母|1
:first-line|p:first-line|选择每个 p 元素的首行|1
:first-child|p:first-child|选择属于父元素的第一个子元素的每个 p 元素|2
:before|p:before|在每个 p 元素的内容之前插入内容|2
:after|p:after|在每个 p 元素的内容之后插入内容|2
:lang(language)|p:lang(it)|选择带有以 "it" 开头的 lang 属性值的每个p元素|2
:first-of-type|p:first-of-type|选择属于其父元素的首个 p 元素|3
:last-of-type|p:last-of-type|选择属于其父元素的最后 p 元素|3
:only-of-type|p:only-of-type|选择属于其父元素唯一的 p 元素|3
:only-child|p:only-child|选择属于其父元素的唯一子元素|3
:nth-child(n)|p:nth-child(2)|选择属于其父元素的第二个子元素|3
:nth-last-child(n)|p:nth-last-child(2)|同上，从最后一个子元素开始计数|3
:nth-of-type(n)|p:nth-of-type(2)|选择属于其父元素第二个 p 元素|3
:nth-last-of-type(n)|p:nth-last-of-type(2)|同上，但是从最后一个子元素开始计数。|3
:last-child|p:last-child|选择属于其父元素最后一个子元素|3
:root|:root|选择文档的根元素|3
:empty|p:empty|选择没有子元素的 p 元素（包括文本节点）|3
:target|#news:target|选择当前活动的 #news 元素|3
:enabled|input:enabled|选择每个启用的 input 元素|3
:disabled|input:disabled|选择每个禁用的 input 元素|3
:checked|input:checked|选择每个被选中的 input 元素|3
:not(selector)|:not(p)|选择非 p 元素的每个元素|3
::selection|::selection|选择被用户选取的元素部分|3
