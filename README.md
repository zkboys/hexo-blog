# hexo-blog
基于hexo搭建的博客 *详细文档请参考[官网](https://hexo.io/)*

## 安装
```
cd hexo-blog
npm install
```
## 修改网站信息
```
# Site
title: ZKBOYS
subtitle: I'm a 博客
description: 技术整理归档
author: WangShubin
language: zh-CN
timezone:
```

## 创建新文章
```
hexo new 'My new Post'

```
将会生成`/source/_posts/My-new-Post.md `文件，内容如下：
```
---
title: My new Post //文章列表标题 网页<title>
date: 2016-03-09 15:59:25
tags:
---
```
## 生成public静态资源（网站的实际内容）
```
hexo generate
```
*删除public目录使用`hexo clean`*

## 发布
修改_config.yml
```
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
  message: [message]
```
安装发布插件
```
npm install hexo-deployer-git --save
```
发布
```
hexo deploy
```
## npm scripts
clean + generate + deploy
package.json中加入
```
"scripts":{
  "deploy":"hexo clean && hexo generate && hexo deploy"
}
```
使用方法
```
npm run deploy
```
