---
title: Git使用
date: 2016-05-31 19:30:04
category: [工具]
tags: [git]
---
[官网地址](http://git-scm.com/)
*git的使用还是挺复杂的，由于精力有限，这里只是总结了一些简单的使用，满足日常工作即可，如果不能满足日常工作，查阅相关资料，再做完善*
## git安装
### linux（ubuntu14）下安装

```
sudo apt-get install git
查看git版本 git --version
```

### windows下安装
```
网上下载一个[git工具](http://rj.baidu.com/soft/detail/30195.html?ald)工具，安装完成即可在windows下使用git
常用的工具为：msysgit
```

### 修改配置
克隆下来的git仓库中有个.git的隐藏文件夹，其中的config文件为git的配置文件，编辑这个config文件可以修改配置。
也可以使用命令进行修改配置：
```
git config --global user.name ...
git config --global user.email ...
git config --global color.ui true :颜色，不设置，默认都是黑色
```

### 可视化工具
[官网](http://www.syntevo.com/smartgit/)
smartgithg分为三个版本：
1. 试用版30天
1. 商业版，需要证书，有技术支持
1. 个人版，不需要证书，没有技术支持

使用时候选择3 个人版。如果选择的是使用版，30天过期后，把home下的隐藏文件夹.smartgit删掉，重新启动smartgit可以重新选择版本

#### PyCharm连接Git
1. File -> Close Project 进入“Welcome to PyCharm ”
1. 点击VCS Check out from Version Control 选择Git

##### 选项说明
1. Vcs Repository URL:(远程Git地址)如ssh://git@192.168.1.136/srv/inc-eking-web.git
1. Parent Directory:拷贝到本地的位置。
1. DirectoryName:文件名称

pycharm本身自带了一些git的使用工具,不太好用,推荐使用smartgit

注：配置3之前生成证书（后续不需要输入密码）


#### git 忽略文件方法
在git文件夹（仓库）下，简历一个.gitignore（隐藏文件）即可。还有其他方法，这个方法，可以吧.gitignore文件提交到服务器上，其他用户可以pull，共享
.gitignore 的语法规范如下：

1. 所有空行或者以注释符号 ＃ 开头的行都会被 Git 忽略；
1. 可以使用标准的 glob 模式匹配。 * 匹配模式最后跟反斜杠（/）说明要忽略的是目录。 * 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。

glob 模式匹配：

1. 星号匹配零个或多个任意字符；
1. [abc] 匹配任何一个列在方括号中的字符（这个例子要么匹配一个 a，要么匹配一个 b，要么匹配一个 c）；
1. 问号（?）只匹配一个任意字符；
1. [0-9a-zA-Z] 在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9a-zA-Z] 表示匹配所有 0 到 9 的数字和所有字母）；
1.  转义字符。

注：理论上来说，在要忽略的格式文件后面添加注释是允许的，但经过我的验证，结果发现这样子操作并不能达到预期的效果。

一个 .gitignore 例子。
````
# 此为注释 – 将被 Git 忽略
# 忽略所有 .a 结尾的文件
*.a
# 但 lib.a 除外
!lib.a
# 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
/TODO
# 忽略 build/ 目录下的所有文件
build/
# 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
doc/*.txt
````

### 分支管理

*分支可以协助不同的开发功能进行，比如发布会单拉出一个分支，bug修改会拉出一个分支，特性开发会拉出一个分支，不同的版本也会拉出一个分支，关于分支怎么管理，根据项目需求适当的拉分支。在分支上进行不同的开发，最总合并到一个分支上（一般是master分支），具体怎么管理分支跟__Git工作流__有关*

### Git工作流
*一个好的工作流方式能很好地管理日常工作，工作流可以理解为分支的checkout与合并？有关工作流相关的资料，网上查阅吧，比较经典的是GitHub工作流？*


### 常用命令
*具体的命令使用请参考[其他网站](http://www.bootcss.com/p/git-guide/)*

#### 创建git仓库
```
sudo git init --bare repertoryname.git
 ```

Git就会创建一个裸仓库(repertoryname)，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以.git结尾。

#### 克隆远程仓库
```
git clone ssh://username@serveraddress:port/repertoryname.git
```

例如：
```
git clone  ssh://git@192.168.0.201/srv/inc-eking-web.git    缺省端口号，默认58001
git clone  ssh://git@xxx.xxx.xxx.xxx:58011/srv/inc-eking-web.git
git clone  ssh://git@www.example.com/srv/inc-eking-web.git   
```

#### 下拉数据
```
git pull origin 分支名
```

例如：
```
git pull origin master
```

#### 提交数据
```
git add --all
git commit -m "My commit"
git push -u origin master
```

#### 开分支
```
git branch 新分支名   
```

例如，在master分支下，新开一个开发分支：
```
git branch dev
```


#### 切换到新的分支
```
git checkout 分支名  
```

例如，在master分支下，切换到新开的dev：
```
git checkout dev
```

#### 开分支和切换分支合并到一个命令
```
git checkout -b 新分支名
```

例如，新开一个开发分支，并立即切换到该分支：
```
git checkout -b dev
```

#### 切换到原分支
```
git checkout 原分支名
```

例如，切换回master：
```
git checkout master   
```

*注意：当前分支有修改，还未commit的时候，会切换失败，应当先commit，但可以不用push*

#### 合并分支
```
git merge 需要合并的分支名
```

例如，刚刚已经切换回master，现在需要合并dev的内容：
```
git merge dev
```

*建议在GitLab(或者其他git系统)上面创建merge request的形式来进行分支的合并和代码审核。*

#### 查看本地分支列表
```
git branch -a   
```

*前面带remotes/origin 的，是远程分支*

#### 查看远程分支列表
```
git branch -r
```

#### 向远程提交本地新开的分支
```
git push origin 新分支名
```

例如，刚刚在master下新开的dev分支：
```
git push origin dev
```

#### 删除远程分支
```
git push origin :远程分支名   
```

例如，删除刚刚提交到远程的dev分支：
```
git push origin :dev
```

#### 删除本地分支
```
git branch 分支名称 -d   
```

例如，在master分支下，删除新开的dev分支：
```
git branch dev -d   
```

*注意：如果dev的更改，push到远程，在GitLab(或者其他git系统)上面进行了merge操作，但是本地master没有pull最新的代码，会删除不成功，可以先`git pull origin master`，或者强制删除：`git branch dev -D`*

#### 更新分支列表信息
```
git fetch -p
```

### git远程仓库搭建
*可以使用git代码托管服务器，git的代码托管服务很多，名气最大的莫过于Github，其他还有GitLab、Bitbucket、CSDN-CODE、Git@OSC等等，如果代码比较重要，可以自己搭建git服务器,假设你已经有sudo权限的用户账号，下面，正式开始安装。*

#### 第一步，安装git：
```
sudo apt-get install git
```

#### 第二步，创建一个git用户，用来运行git服务：
```
sudo adduser git
```

#### 第三步，创建证书：
证书的作用：一些软件(比如git)要请求远程机器上的数据,可以使用证书,就不用每次请求数据时都输入远程机器的用户名和密码了.

1. 终端根目录中输入：ssh-keygen -t rsa -C "wangshubin@eking.mobi" 然后一路回车
1. 进入.ssh目录 cd ~/.ssh   (~是根目录)
1. cat id_rsa.pub
1. 远程连接其他机器：ssh eking@xxx.xxx.xxx.xxx 或者  sshpass -p 'xxxxx' ssh admin@xxx.xxx.xxx.xxx （可以将此条命令建成sh文件，如果有很多远程机器需要维护，这样可以方便链接）
1. 进入远程机器的.ssh目录   cd /home/git/.ssh
1. vi编辑authorized_keys文件(一般.ssh目录下就这一个文件) 将3步中生成的key添加到authorized_keys文件中，一行一个


*注:cd /home/git/.ssh(git指的是用户名,每个用户下会有一个.ssh文件夹,这个文件夹只有经过相应的ssh操作才会存在,不存在可以手动添加一个,authorized_keys文件如果不存在可以添加一个.)*

#### 第四步，初始化Git仓库：
先选定一个目录作为Git仓库，假定是/srv/sample.git，在/srv目录下输入命令：
```
sudo git init --bare sample.git
```

*Git就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以.git结尾。*

然后，把owner改为git，让这个目录可以通过git用户访问：
```
sudo chown -R git:git sample.git
```

#### 第五步，禁用shell登录：
出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑/etc/passwd文件完成。找到类似下面的一行：
```
git:x:1001:1001:,,,:/home/git:/bin/bash
```

改为：
```
git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
```

这样，git用户可以正常通过ssh使用git，但无法登录shell，因为我们为git用户指定的git-shell每次一登录就自动退出。

#### 第六步，克隆远程仓库：
现在，可以通过git clone命令克隆远程仓库了，在各自的电脑上运行：

```
git clone git@server:/srv/sample.git
```

显示如下信息表明成功（前提这个库是空的）：
```
Cloning into 'sample'...
warning: You appear to have cloned an empty repository.
```

#### 其他
1. 要方便管理公钥，用Gitosis；
1. 要像SVN那样变态地控制权限，用Gitolite。
