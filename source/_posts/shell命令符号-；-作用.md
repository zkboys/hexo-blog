---
title: 'shell命令符号& && ； ||作用'
date: 2016-06-21 18:01:20
category: [后端, shell]
tags: [mongodb]
---
## 符号`&`
多个命令同时执行。
```
command1&command2&command3
```

## 符号`&&`
顺序执行，只有前面的命令执行成功，后面的命令才会执行。
```
command1&&command2&&command3
```
## 符号`；`
书序执行，不管前面得命令是否成功，后面的命令继续执行。
```
command1;command2;command3
```
## 符号`||`
前面命令如果执行成功，不执行后面的命令，失败则执行后面的命令。
```
command1||command2||command3
```

注：&& 和 || 与程序的逻辑运算含义一致。
