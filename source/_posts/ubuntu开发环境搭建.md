---
title: ubuntu开发环境搭建
date: 2016-08-24 15:27:10
category: [工具]
tags: 环境搭建
---
开发环境搭建：
## git
```bash
sudo apt-get install git
```
## 生成ssh key
- 生成key，执行如下命令，然后一路回车即可
	```bash
	ssh-keygen -t rsa -C “xxx@163.com”
	```
- 复制id_rsa.pub中内容到远程服务器
	```bash
	cd ~/.ssh
	cat id_rsa.pub
	```
- 进入远程服务器，编辑authorized_keys文件，加入生成的id_rsa.pub
	```
	vi /home/git/.ssh/authorized_keys
	```

## 安装nodejs
```bash
sudo apt-get install -y build-essential
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo ln -s /usr/bin/nodejs /usr/bin/node
```
## 升级npm
```bash
sudo npm update npm -g
```
## 安装java8
```bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer -y
java -version
```

## 安装maven3
[官方](http://maven.apache.org/download.cgi)下载最新的apache-maven-3.x.y-bin.tar.gz
```bash
解压
sudo tar zxvf apache-maven-3.3.9-bin.tar.gz -C /usr/local/

sudo vi /etc/profile
加入：export PATH=/usr/local/apache-maven-3.3.9/bin:$PATH

注销后：
mvn -v

```
