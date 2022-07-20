---
layout: post
title: 记录基于pyqt编写的图片处理小工具
date: 2022-7-20
categories: blog
tags: [pyqt,python,opencv]
description: [Error]
---

开坑记录自己编写image处理小工具的过程  
起因是每次对图片进行resize 裁剪等操作的时候找不到合适的工具就打开了Ps  
然而我觉得这种小的调整根本用不着兴师动众用上Ps，再者对我这种初学者Ps的操作是比较陌生的  
大一玩opencv库的时候感受到这个库能够很方便高效的对图片进行各种操作，就想着用一个可视化Gui的形式把部分代码封装成一个小工具  

# Mission 1 : 文件的打开、保存等功能

### 重大问题
1.opencv imread读取硬盘文件的问腿
# Mission 2 : 完成resize功能
# Mission 3