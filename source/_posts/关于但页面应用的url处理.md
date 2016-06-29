---
title: 关于单页面应用的url处理
date: 2016-06-29 18:16:45
category: [实现方案]
tags: [单页面]
---
单页面应用越来越流行，单页面应用的开发页面跳转都需要前端来处理，配合H5的history API，可以不使用hash方式拼接url，但是带来一个问题，如果用户刷新当前页面，通过history修改过的url会正常的发送请求到后端，如果后端不做处理，就会返回404，用户体验不是很好。

## 单页面应用url处理方式
一般的单页面应用，都会使用一个前端router统一控制跳转，很少会自己通过history实现逻辑，一般成熟router都会提供hash，和history两种方式修改url。
- hash方式，地址栏会拼接#xxx，后端不需要特殊配置，刷新前进后退等history相关操作都OK，但是地址栏也比较丑陋，无法使用锚点
- history方式，通过pushState，replaceState改变地址栏，看起来就跟真实的地址一样，对于有url洁癖的同学来说，perfect！但是刷新需要后端做特殊支持

## history方式，后端支持
后端如果发现是get请求，并且没有被处理，都跳转到index。
- 通过服务器实现

```
Apache
In your vhost :

<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteBase /
    RewriteRule ^index\.html$ - [L]
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule . /index.html [L]
 </IfModule>
```
```
Nginx
rewrite ^(.+)$ /index.html last;
```
- 通过代码实现可以在后端路由处做处理，所有未截获的get请求（非ajax请求），都跳转到index

个人比较喜欢代码方式，灵活性比较高，而且不用修改服务器配置

这样处理过，后端就不会存在404，将控制权交给了前端，当通过一个url进入页面时，后端统一跳转到index，前端通过路由匹配是否有对应页面，如果没有，前端跳转404

参考链接：
http://readystate4.com/2012/05/17/nginx-and-apache-rewrite-to-support-html5-pushstate/
