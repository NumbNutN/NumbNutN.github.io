---
layout: post
title: 记录学习图像处理的图片属性[位深度/通道数/颜色模式]
date: 2022-7-20
categories: blog
tags: [pyqt,python,opencv]
description: [Error]
---

## 记录图像处理的学习

了解图像的几个属性
位深度

opencv-python库存储图像的形式为numpy的数组类型ndarray
ndarray的几个属性

shape：如果是彩色图像，获取图像的形状，返回包含行数、列数、通道数的数组；如果是二值图像或者灰度图像，则仅返回行数和列数。  


通过该属性的返回值是否包含通道数，可以判断一幅图像是灰度图像（或二值图像）还是彩色图像。

size：返回图像的像素数目。其值为“行×列×通道数”，灰度图像或者二值图像的通道 数为 1。

dtype：返回图像的数据类型
uint8  --单个元素占8个字节
float64 --数组中每个元素为64bits的浮点数，即8个字节

[OpenCV获取图像属性](https://blog.csdn.net/weixin_51571728/article/details/120716708)
img = cv2.imread("image.png",flags=cv2.CV_8UC4)

矩阵类型
CV_8UC1 8位无符号整型单通道矩阵，灰度图GrayScale以这种形式存储
CV_8UC3 8位无符号整型三通道矩阵，主流RGB模式24位图以这种矩阵形式存储，即一个像素点RGB三个颜色分量各由8个bits，1个字节表示，共24位
CV_8UC4 8位无符号整型四通道矩阵，ARPG模式32位图以这种形式存储，图像相比CV_8UC3多出一个Alpha通道，多用一个字节0-255表示透明程度
CV_32FCx 一般的图像格式(png,jpg等)只用整数类型保存图片信息，一般不会用这种格式加载

对应关系
QImage.Format_BGR888 对应 CV_8UC3
QImgae.Format_ABGR32 对应 CV_8UC4

这两种方式都会在加载中丢弃图像的颜色信息，加载灰度图
img = cv2.imread("image.png",flags=cv2.IMREAD_GRAYSCALE)
img = cv2.imread("image.png",flags=cv2.CV_8UC1)

这种方式加载绝大多数.jpg格式，因为jpg格式丢失图片的透明度信息
img = cv2.imread("image.png",flags=cv2.CV_8UC3)
img = cv2.imread("image.png",flags=cv2.IMREAD_COLOR)


这种方式加载绝大多数.png格式，png图24位图和32位图
测试发现
img = cv2.imread("image.png",flags=cv2.CV_8UC4)

实际测试
发现很奇怪的现象，选取一张分辨率200x200,通道8位的32位图用opencv打开
img = cv2.imread("image.png",flags=cv2.CV_8UC1)
得到(200,200)
img = cv2.imread("image.png",flags=cv2.CV_8UC2)
得到完全正确的(200,200,4)
img = cv2.imread("image.png",flags=cv2.CV_8UC3)
(100,100,3),丧失透明度信息，图片缩小为原来的1/4
img = cv2.imread("image.png",flags=cv2.CV_8UC4)
(100,100,4)，透明度未丢失，图片缩小为原来的1/4
img = cv2.imread("image.png",flags=cv2.IMREAD_COLOR)
img = cv2.imread("image.png")
(200,200,3)，透明度丢失，尺寸正常
img = cv2.imread("image.png",flags=cv2.IMREAD_UNCHANGED)
得到完全正确的(200,200,4)


色深/位深，表示在位图或者视频帧缓冲区中储存1像素的颜色所用的位数，它也称为位/像素（bpp）
https://zhuanlan.zhihu.com/p/71155212


