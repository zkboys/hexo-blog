---
title: emmet语法
date: 2016-03-11 14:35:53
category: [工具]
tags: emmet
---
## `element`标签名
```
div
...will produce:
<div></div>
```
## `ID`id选择符
```
div#some-id 或者 #some-id
...will produce:
<div id="some-id"><div>
```
## `CLASS`类选择符
```
div.some-class 或者 .some-class
...will produce:
<div class="some-class"></div>
```
## `>` 嵌套，直接子节点
```
div>ul>li
...will produce:
<div>
    <ul>
        <li></li>
    </ul>
</div>
```
## `+`兄弟节点
```
div+p+bq
...will produce:
<div></div>
<p></p>
<blockquote></blockquote>
```
## `^`切换上下文，返回上一级
```
div+div>p>span+em^bq
...will produce:
<div></div>
<div>
    <p><span></span><em></em></p>
    <blockquote></blockquote>
</div>
```
### 可以多个一起使用，每一个返回一级
```
div+div>p>span+em^^^bq
...will produce:
<div></div>
<div>
    <p><span></span><em></em></p>
</div>
<blockquote></blockquote>
```
## `*` 重复多个
```
ul>li*5
...will produce:
<ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
</ul>
```
## `()`分组，用来分组子集，不推荐过多使用
```
div>(header>ul>li*2>a)+footer>p
...will produce:
<div>
    <header>
        <ul>
            <li><a href=""></a></li>
            <li><a href=""></a></li>
        </ul>
    </header>
    <footer>
        <p></p>
    </footer>
</div>
```
### `()`可以嵌套使用
```
(div>dl>(dt+dd)*3)+footer>p
...will produce:
<div>
    <dl>
        <dt></dt>
        <dd></dd>
        <dt></dt>
        <dd></dd>
        <dt></dt>
        <dd></dd>
    </dl>
</div>
<footer>
    <p></p>
</footer>
```
## `[]`用户自定义属性
```
div[title="Hello world!"]
...will produce:
<div title="Hello world!" data-name="haha"></div>
```
### 说明：
- 方括号内可以一次性写多个属性，以空格隔开，比如：[title='H W' data-name=haha]
- 属性可以不写属性值，比如：[title data-name]
- 属性值可以使用单引号或者双引号
- 属性值如果没有空格，可以省略引号

## `$`数字
```
ul>li.item$*5
...will produce:
<ul>
    <li class="item1"></li>
    <li class="item2"></li>
    <li class="item3"></li>
    <li class="item4"></li>
    <li class="item5"></li>
</ul>
```
### 可以使用多个`$`，不足会使用`0`站位
```
ul>li.item$$$*5
...will produce:
<ul>
    <li class="item001"></li>
    <li class="item002"></li>
    <li class="item003"></li>
    <li class="item004"></li>
    <li class="item005"></li>
</ul>
```
### `@`控制数字开始值和顺序
#### `@-` 倒序
```
ul>li.item$@-*5
...will produce:
<ul>
    <li class="item5"></li>
    <li class="item4"></li>
    <li class="item3"></li>
    <li class="item2"></li>
    <li class="item1"></li>
</ul>
```
#### `@n` 改变数字开始位置
```
ul>li.item$@3*5
...will produce:
<ul>
    <li class="item3"></li>
    <li class="item4"></li>
    <li class="item5"></li>
    <li class="item6"></li>
    <li class="item7"></li>
</ul>
```
#### `@-n` 降序并改变开始位置
```
ul>li.item$@-3*5
...will produce:
<ul>
    <li class="item7"></li>
    <li class="item6"></li>
    <li class="item5"></li>
    <li class="item4"></li>
    <li class="item3"></li>
</ul>
```
## `{}`文本节点
```
a{Click me}
...will produce:
<a href="">Click me</a>
```
### 注意如下的区别（受`>`影响）
```
a{click}+b{here}
...will produce:
<a href="">click</a><b>here</b>

a>{click}+b{here}
...will produce:
<a href="">click<b>here</b></a>
```
## 缺省表签名
```
#some-id                  div#some-id
.some-class               div.some-class
.wrap>.content            div.wrap>div.content
em>.info                  em>span.info
ul>.item*3                ul>li.item*3
table>#row$*4>[colspan=2] table>tr#row$*4>td[colspan=2]
```
### 缺省标签名之后，emmet会根据父级标签确定表签名，一些例子：
- li for ul and ol
- tr for table, tbody, thead and tfoot
- td for tr
- option for select and optgroup

## `lorem` 生成一段虚拟文字，一般用来快速填充html，查看效果
```
lorem
...will produce:
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias et nemo repudiandae. Esse ex molestias numquam, possimus quaerat quas sint tempora? Asperiores dicta ducimus facilis impedit neque ratione ut vel!

lorem10 //生成10个单词
...will produce:
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolore, totam.

p*4>lorem
...will produce:
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Qui dicta minus molestiae vel beatae natus eveniet ratione temporibus aperiam harum alias officiis assumenda officia quibusdam deleniti eos cupiditate dolore doloribus!</p>
<p>Ad dolore dignissimos asperiores dicta facere optio quod commodi nam tempore recusandae. Rerum sed nulla eum vero expedita ex delectus voluptates rem at neque quos facere sequi unde optio aliquam!</p>
<p>Tenetur quod quidem in voluptatem corporis dolorum dicta sit pariatur porro quaerat autem ipsam odit quam beatae tempora quibusdam illum! Modi velit odio nam nulla unde amet odit pariatur at!</p>
<p>Consequatur rerum amet fuga expedita sunt et tempora saepe? Iusto nihil explicabo perferendis quos provident delectus ducimus necessitatibus reiciendis optio tempora unde earum doloremque commodi laudantium ad nulla vel odio?</p>

ul.generic-list>lorem10.item*4  //10是只每行10个单词
...will produce:
<ul class="generic-list">
    <li class="item">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nam vero.</li>
    <li class="item">Laboriosam quaerat sapiente minima nam minus similique illum architecto et!</li>
    <li class="item">Incidunt vitae quae facere ducimus nostrum aliquid dolorum veritatis dicta!</li>
    <li class="item">Tenetur laborum quod cum excepturi recusandae porro sint quas soluta!</li>
</ul>
```
## 注意：
- 空格是emmet停止转换的分隔符，一个emmt语句中，不能有空格
- 不要写太复杂的语法，写太复杂了容易出错。

## 参考连接
[http://docs.emmet.io/](http://docs.emmet.io/)
[http://emmet.evget.com/](http://emmet.evget.com/)
