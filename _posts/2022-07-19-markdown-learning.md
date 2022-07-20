---
layout: post
title: 学习markdown
date: 2022-7-19
categories: blog
tags: [第一次,耶喜]
description: 文章金句。
---

### 作为啥也不懂的计算机科班大一萌新，这个博客的网站搭建包括模板都参考自“独立写生”发布的博客搭建教程
教程原文：[如何搭建个人独立博客？ --知乎](https://www.zhihu.com/question/20463581/answer/51381121)  
在此致谢，正是这些行业的大佬们本着伟大的共享精神分享自己的技术栈让我们这些学习计算机的新人们找到了引路的灯塔  
由于这个博客模板推送新博文使用的是markdown语法  
这篇博文开坑来记录一下markdown语法的学习  

## 标题 
上面就是一个标题，在设置为标题的文字前加上#即可，不同数量代表不同的标题级数 
>\# 这是一级标题 <br>
>\#\# 这是二级标题 <br>
>\#\#\# 这是三级标题 <br>
>\#\#\#\# 这是四级标题 <br>

效果： 
# 这是一级标题
## 这是二级标题
### 这是三级标题
<br>

## 换行
在markdown语法中，两个空格+一个换行符即可表示换行  
>我生长在一个特别普通的家庭  
从小特别自卑

效果：  
我生长在一个特别普通的家庭  
从小特别自卑  

只换行不加空格的效果：  
我生长在一个特别普通的家庭 
从小特别自卑 

两个回车键不加空格的效果：  
我生长在一个特别普通的家庭

从小特别自卑 

内容来源：[markdown换行命令 --腾赚](https://www.tengzhuan.com/post/79724.html)  

## 引用
>(>这是引用的内容) <br>
>(>>这是引用的内容) 

效果：  
>这是引用的内容 
>>这是引用的内容 

### 引用的结束 
空行结束（两个回车键） 
用新的标题或者新的列表结束 
内容来源：[Markdown如何结束引用 --简书](https://www.jianshu.com/p/74d911639a5f?u_atoken=d90bf373-0085-4de5-ae7b-6b19266269a6&u_asession=014QmQa5HNhcSKVkOhT0UiVGXVtiR92nLCaQ-x1Q7mpA5NlQZs_I6emPbkPooA2kFzX0KNBwm7Lovlpxjd_P_q4JsKWYrT3W_NKPr8w6oU7K9Tihgf4DX6KMD4hLMKqljMPpcarp92QKzyJKyYjREPlmBkFo3NEHBv0PZUm6pbxQU&u_asig=05NvLLX17Yh0EcOR5Ex57VXa8c7lMPSHMDr0f3M9C4iat2PsXsfGElTsQwhbgsecHqVGKWl18Fw8xSdv89ACN8mx0duCxl7mRpikBJ6yENkUsuzMF7vRBn5leNVe2h0V9c4oRnjt9-rJZi2bbtpcKuVdoBrYT-Oh2K4hyXE8pzbtj9JS7q8ZD7Xtz2Ly-b0kmuyAKRFSVJkkdwVUnyHAIJzcO0_46EFjqnC08JBRykx9C-GtvBh0zX_eXzrIN9SpANWPRPQyB_SKrj-61LB_f61u3h9VXwMyh6PgyDIVSG1W98FNlKAV3VAum3ev36sKet0lxEO2egZLn_KjcvC2APzMUmGzkA6VIIo0tK9bDVaQt0LWfvFHNx4JUxAUD2iBGsmWspDxyAEEo4kbsryBKb9Q&u_aref=mNLRhiyWonDSJzG83aS1ZZADZcY%3D)

### 引用的换行
引用的内容用一个空格+一个换行符换行似乎是无效的 
需要往一行文本加入换行标签\<br\>

## 代码
单行代码：代码之间用反引号包起来 (注意，是反引号不是单引号噢，反引号在键盘的位置按住shift可以打出"~")  
>\`代码内容\` 

效果： 
`代码内容` 

多行代码：多行代码用\`\`\`三个反引号括住 
>\`\`\` <br>
function fun(){ <br>
    console.log("牛逼哄哄的代码); <br> 
} <br>
\`\`\` 

效果： 
```
    function fun(){
        console.log("牛逼哄哄的代码);  
    }
```

## 超链接
语法：
>\[超链接名\]\(超链接地址 "超链接title"\) <br>
\[BLOG --numbnut.bond\]\(numbnut.bond "我的博客 --numbnut.bond"\) <br>

效果： 
[BLOG --numbnut.bond](numbnut.bond "我的博客 --numbnut.bond") 

## 














