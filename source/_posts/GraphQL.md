---
title: GraphQL
date: 2017-04-02 09:03:55
category: [工具]
tags: [GraphQL]
---
## GraphQL

[中文官网](http://graphql.cn/)

[英文官网](http://graphql.org/)

[React Apollo](https://github.com/apollographql/react-apollo)

1. 对API中的数据提供了一套易于理解的完整描述；
2. 客户端可以准确的获取所需数据，所需结构，前端可定制性较强，所需数据基本可以自己组织；
3. 获取的数据没有冗余，后端也会有相应得性能优化（不获取的字段，不会执行后端相应得解析函数）；
4. API容易演进，提供不同版本的数据；
5. 一个请求获取多个资源，降低HTTP请求数量；
6. 容易提供强大的开发工具；
7. 以模块为单位进行数据组织；（如何划分是个难点）

## restful api

目前我们项目存在的问题：

1. 字段没有中文描述，不常见字段不知道对应的是什么；
2. 不同人开发的、不同接口中，同一内容，命名不同，比如 【房号】有的人（接口）中为roomNum,有的为roomNo；
3. 有的接口返回的数据并不利于前端展示，前端需要做转换；
4. 接口是哪位后端开发的并不知道、是否开发完成也不知道；
5. 日期相关参数，格式不统一；
6. swagger 文档中接口越来越多，查找有些困难；
7. 很多数据存在无意义前缀，比如roomType : {roomTypeId, roomTypeName, ...}，这里直接写成：roomType:{id, name, ...}，使用时，一般形式为：roomType.id, roomType.name，没个字段就不必添加前缀，显得冗余；





