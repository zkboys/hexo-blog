# hexo-blog
基于hexo搭建的博客 *详细文档请参考[官网](https://hexo.io/)*

## 安装
```
npm install hexo-cli -g
git clone https://github.com/zkboys/hexo-blog.git
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
  "deploy":"hexo clean && hexo generate && hexo deploy",
  "push":"git add --all && git commit -m 'blog update' && git push origin master",
  "done":"npm run push && npm run deploy"
}
```
使用方法
```
发布
npm run deploy
提交
npm run push
提交并发布：
npm run done
```
一般使用`npm run done`命令，提交并发布．
*注：如果项目没有任何更改，调用npm run push命令会报错*
