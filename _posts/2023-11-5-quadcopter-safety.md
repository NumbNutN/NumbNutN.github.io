---
layout: post
title: 四轴调试安全守则
date: 2023-11-6
categories: blog
tags: [四轴飞行器设计]
description: None
---


### 硬件规范

1) 检查电机底座螺丝是否拧紧
>底座不稳可能导致电机脱出，绞断线缆 。

<img src="https://raw.githubusercontent.com/NumbNutN/NumbNutN.github.io/main/img/post-img/for-safety-screws.jpg" alt="for-safety-screws" style="zoom:33%;" />

1) 检查电机桨夹（子弹头）是否拧紧，请使用质地较硬的扳手顺时针拧紧，切勿用手拧紧
>未拧紧容易导致桨夹和螺旋桨甩出，造成严重后果。

<img src="https://raw.githubusercontent.com/NumbNutN/NumbNutN.github.io/main/img/post-img/for-safety-bullet.jpg" alt="for-safety-bullet" style="zoom:33%;" />

3) 为螺旋桨加装保护圈，有效防止螺旋桨和外部环境发生碰撞

<img src="https://raw.githubusercontent.com/NumbNutN/NumbNutN.github.io/main/img/post-img/for-safety-blade-protection.jpg" alt="for-safety-blade-protection" style="zoom:33%;" />

4) 为电源和动力系统的供电加装拨动开关，在软件控制失效时紧急切断动力源

<img src="https://raw.githubusercontent.com/NumbNutN/NumbNutN.github.io/main/img/post-img/for-safety-switch.jpg" alt="for-safety-switch" style="zoom:33%;" />

5) 减少飞线，使用轧带或绝缘胶带收纳飞线

> 杂乱无章的飞线可能卷入螺旋桨造成严重损失


### 软件规范

1) 使用一个遥控器通道或其他远程控制信号设置油门行程，机动可控，避免将电调油门行程设置流程放置于复位中断服务例程
> 以脉宽调制信号（PWM）为例，无刷电子调速器设置油门行程流程往往要求先产生最高油门行程信号并保持一段时间后，产生最小油门行程信号，对不处于油门行程设置状态的电调的设置行为可能造成严重后果。

2) 编写电调驱动时，采用规范良好的软件设计模式，为油门设置最大行程阈值



### 良好习惯

1) 调试时确保现场有两人或以上相互协助，手部可以够到制动装置（遥控器、电源开关等），保证场地空旷，远离飞行器

2) 动力控制和驱动代码发生变动时，评估有关风险，提高相关安全防护等级

3) 调试流程统一有序，每次完成一轮无人机调试后，切断动力源

4) 关注电池状态，为电池加装电压监测报警器

<img src="https://raw.githubusercontent.com/NumbNutN/NumbNutN.github.io/main/img/post-img/for-safety-beep.jpg" alt="for-safety-beep" style="zoom:33%;" />
