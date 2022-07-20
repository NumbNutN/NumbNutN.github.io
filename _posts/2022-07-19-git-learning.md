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


## Vim语法
git命令窗的文本编辑模式使用的是vim语法，熟悉基本的语法可以帮助你提高使用git进行commit描述时的效率  
insert/i 进入插入模式  
Esc 结束插入模式  
:wq+Enter 在命令模式输入该指令来保存并结束本次操作 
yy 复制一行
p 粘贴 
资料来源：
[学习vim语法 --CSDN](https://blog.csdn.net/qq_27127385/article/details/103627332)  
[git pull时提示…… --CSDN](https://blog.csdn.net/qq_29590623/article/details/87614505)  
其他快捷键：  
ctrl+i 清屏  

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
>2021年8月13日后Github不再支持用户名密码的方式验证，需要创建个人访问令牌(personal access token)，并以上述代码的格式添加到你的remote库链接中  
按照下方教程的方式设置个人访问令牌  
资料来源：  
[【突发】解决remote: Support for password authentication was removed on August 13, 2021. Please use a perso](https://helloai.blog.csdn.net/article/details/119696726?spm=1001.2014.3001.5506)  

```
#当本地分支名在远程库不含有时，将会新建一个新的分支？存疑
git pull origin master

#当本地不含有这个分支名，就会报错
```

### 添加到暂存区 
```
git add <filename>
//添加当前路径所有的文件
git add .
git add --all
```


别名相当于一个指向你github远端仓库的一个指针  
在你进行一次git clone操作时，git将自动将别名“origin”关联到你克隆的远程仓库  
这也是为什么git的push 和pull的常见写法有  
```
git push -u origin main/master  
git pull origin master
```

### 为远程库添加别名
```
git remote add <NICKNAME> <REPO>
git remote add blogRepo https://github.com/<USERNAME>/<REPO>.git 
//以后同样可以启用你自定义的别名了
git push -u blogRepo main
```  

### 删除别名
`git remote remove <NICKNAME>`  
需要注意的是，别名的配置是存储在你的当前git工作路径下的，当你换到另一个local repository时，你的别名配置需要重新弄

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
\# Please enter a commit message to explain why this merge is necessary,  
\# especially if it merges an updated upstream into a topic branch.  
\#  
\# Lines starting with '#' will be ignored, and an empty message aborts  
\# the commit.  
102这个情况出现于pull远程库时你的本地库已经有改动，需要代码merge的时候要求说明


error: src refspec main does not match any
error: failed to push some refs to 'https://github.com/NumbNutN/aUnfinishedImageEditTool.git'



## VsCode与git配合状态显示
[vscode-git中的U,M和D文件标记的含义 --CSDN](https://blog.csdn.net/qq_43827595/article/details/100393316)  

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

## 参考文章
[详解Git工作区…… --程序员大本营](https://www.pianshen.com/article/377153309/)  
[GitHub提交的时显示Updates were rejected because the remote contains work that you do --CSDN](https://blog.csdn.net/u012308586/article/details/104905828?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-0-104905828-blog-112171133.pc_relevant_sortByStrongTime&spm=1001.2101.3001.4242.1&utm_relevant_index=3)  
[【突发】解决remote: Support for password authentication was removed on August 13, 2021. Please use a perso --CSDN](https://helloai.blog.csdn.net/article/details/119696726?spm=1001.2014.3001.5506)  
[Git 常见错误 之 error: src refspec xxx does not match any / error: failed to push some refs to 简单解决方法 --CSDN](https://blog.csdn.net/u014361280/article/details/109703556)  
[关于git的问题：error: src refspec main does not match any --CSDN](https://blog.csdn.net/gongdamrgao/article/details/115032436)  














