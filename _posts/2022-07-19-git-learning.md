---
layout: post
title: 学习git指令
date: 2022-7-19
categories: blog
tags: [git,技术]
description: 文章金句。
---

### 这篇博文总结一下自己的git指令学习内容防忘记

git是一个分布式版本控制系统   
git可以被简单的分为三个区域  
工作区(Working Directory)
暂存区(Stage index)  
历史记录区(History)


## 语法
insert 进入插入描述模式  
Esc 结束插入描述模式  
:wq+Enter 在命令模式输入该指令来保存并结束本次操作  
资料来源：[git pull时提示…… --CSDN](https://blog.csdn.net/qq_29590623/article/details/87614505)

### 初始化本地库
init 在一个路径打开git bash后，初始化本地库后使git获得这个目录的管理权，包括该目录下的所有子目录，Windows系统的文件资源管理器在"显示隐藏文件"的勾选情况下可以看到.git文件夹

```
git init
```

## 克隆库
clone是在本地没有repository时，将远程repository整个下载下来
```
git clone https://github.com/<USERNAME>/<REPO>.git
```

### 拉取库
pull将远程repository里新的commit数据下过过来，与本地代码merge  
这将会把新的代码直接添加到你的工作区
```
git pull https://<your_token>@github.com/<USERNAME>/<REPO>.git 分支
```

### 添加到暂存区 
```
git add <filename>
//添加当前路径所有的文件
git add .
git add --all
```

## 一些常见的信息



error: RPC failed; curl 28 OpenSSL SSL_read: Connection was aborted, errno 10053
fatal: the remote end hung up unexpectedly
fatal: the remote end hung up unexpectedly
Everything up-to-date
104目前这个错误往往只因为梯子不好网络连接不好


 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'https://github.com/<USERNAME>/<REPO>'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.  
101这个错误是由于远程库在距你上一次push你的分支以后信息有变动，需要拉取远程库和你的本地代码merge后再push


Merge branch 'master' of https://github.com/NumbNutN/TestRepo
# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.
102这个情况出现于pull远程库时你的本地库已经有改动，需要代码merge的时候要求说明


## Test

2022_7_19_23:41 在本地repo新建文件test.txt
2022_7_19_23:53 在remote里新建文件README.md
2022_7_19_23:59 尝试把本地push到远程，报错101
2022_7_20_0:01 把remote拉取到本地，本地工作区新增文件README.md

下一步计划：两边库分别作进一步修改模拟merge冲突
2022_7_20_0:07 remote新commit txt文件remote_code.txt
2022_7_20_0:09 local新commit文件 local_code.txt
2022_7_20_0:10 尝试把localpush到remote，报错101
2022_7_20_0:16 把remoteRepo Pull到local 出现102，要求说明merge的必要性
2022_7_20_0:16 本地新增文件remote_code.txt















