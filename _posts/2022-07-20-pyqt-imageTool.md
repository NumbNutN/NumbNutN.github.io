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
1.opencv imread读取硬盘文件的问题
opencv imread()函数不支持中文路径！ 接收中文路径函数就会返回"None",对于我们大部分中文使用者这显然是难以接收的
>解决的思路就是先用其他支持中文的API，把图片数据导入到内存中，然后通过opencv从内存读入图片的方法，读入图片。
```
import cv2
import numpy as np

def readimg(filename, mode):
	raw_data = np.fromfile(filename, dtype=np.uint8)  #先用numpy把图片文件存入内存：raw_data，把图片数据看做是纯字节数据
	img = cv2.imdecode(raw_data, cv2.IMREAD_COLOR)  #从内存数据读入图片
	return img
```
一些资料： 
[opencv中的imread不支持中文路径的解决办法 --CSDN](https://blog.csdn.net/WhoisPo/article/details/104511841/)   
[OpenCV-Python cv2.imdecode()和cv2.imencode() 图片解码和编码 --CSDN](https://blog.csdn.net/dcrmg/article/details/79155233)  

2.保存最近打开文件的路径

# Mission 2 : 完成resize功能

### 重大问题
1.将opencv的文件格式(np.ndarray)转化为Qimage格式时图片歪斜，严重时程序异常退出
```
def ShowPic(cvImg, label):
    showImg = QImage(cvImg.data, cvImg.shape[1], cvImg.shape[0], QImage.Format_RGB888)
    label.setPixmap(QPixmap.fromImage(showImg))
```

```
def ShowPic(cvImg, label):
    showImg = QImage(cvImg.data, cvImg.shape[1], cvImg.shape[0], cvImg.shape[1]*3, QImage.Format_RGB888)
    #   5.在PYQT5显示，需要转化为QPixmap格式
    label.setPixmap(QPixmap.fromImage(showImg))
```


解决方法：[Qt中用QLabel显示OpenCV中Mat图像数据出现扭曲现象的解决 --CSDN](https://blog.csdn.net/loveaborn/article/details/7680834)
原因：
缺省了一个参数bytePerLine造成图像显示异常
显然这里默认采用的24位色深，RGB三个通道每个各用3个字节存储，因此每行的字节数为shape[1]*3



简单叙述一下图片的全流程：
1.
```
raw_data = np.fromfile(filePath,dtype=np.uint8)
img = cv2.imdecode(raw_data,cv2.IMREAD_COLOR)
```
这里调用了numpy的api来确保支持中文
再转化成opencv

这里提到了用Qimage的API读取图片的方法[解决OpenCV的imread/imwrite在Qt环境不支持中文路径的问题 --CSDN](https://blog.csdn.net/libaineu2004/article/details/125350118)
2.
```
img2=cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
```
这里是因为opencv图片以BGR的通道顺序存储，而QImage中使用的是RGB形式，因此要使用cvtColor进行转换  
[Pyqt QImage 与 np array 转换 --CSDN](https://blog.csdn.net/ccchen706/article/details/71425653)
[Qt中用QLabel显示OpenCV中Mat图像数据出现扭曲现象的解决 --CSDN](https://blog.csdn.net/loveaborn/article/details/7680834)

3.
```
img3 = QImage(img2.data, img2.shape[1], img2.shape[0], QImage.Format_RGB888)
这一步将opencv格式的图片转化成QImage
```
4.
```
img4 = QPixmap.fromImage(img3)
label.setPixmap(img4)
最后一步将Qimage转化为专为屏幕显示设计的QPixmap格式
```
这个链接可以更详细的了解Qt提供的几种图片格式：[QPixmap、QImage、QPicture、QBitmap四者区别](https://blog.csdn.net/luoyayun361/article/details/123366133)


# Mission 3 ：完成描边转换功能

### 重大问题
原有思路是为负责描边功能的python类class EdgeDetection设置两个类的属性  
- tempSobelImg 负责存储由sobel算子进行一次计算得到\[边缘 白\]\[填充 黑\]  
- tempFlipImg 负责存储由tempSobelImg反转后得到的\[边缘 黑\]\[填充 白\]  
属性定义方法如下：  
```
class EdgeDetection:

    tempSobelImg = None
    tempFlipImg = None

    def __init__(self):
    ...
```
对图像进行反转的方式如下：
```
    def FlipImg(self,img):
        newImg = img
        i = 0
        j = 0
        while i < newImg.shape[0]:
            while j < newImg.shape[1]:
                newImg[i][j] = 255 - img[i][j]
                j += 1
            j = 0
            i += 1
        return newImg
```

```
    def FindEdge(self):
        if (SI.ui.cBoxCvtMargin.isChecked()):
            sobelx = cv2.Sobel(SI.showCvImg[0], -1, 1, 0, ksize=3)
            sobely = cv2.Sobel(SI.showCvImg[0], -1, 0, 1, ksize=3)
            self.tempSobelImg = cv2.addWeighted(sobelx, 0.5, sobely, 0.5, 0) #步骤I.sobel算子处理得到
            self.tempFlipImg = self.FlipImg(self.tempSobelImg) #步骤II.把翻转后的图片存储在EdgeDection.tempFlipImg内
            SI.showCvImg[0] = self.tempSobelImg
        else:
            SI.showCvImg[0] = SI.showCvImg[1]
        SI.ShowPic(SI.showCvImg[0], SI.ui.labelShowImg)
```
结果发现  
在上述代码处理到\[II.步骤二\]后，tempSobelImg和tempFlipImg的内容物竟然是一致的，存储的是反转后的图像！  
最后的原因竟是...  
```
def FlipImg(self,img):
        newImg = img
```
numpy模块ndarray数据类型的赋值运算=是浅拷贝，将img的地址赋给了newImg，而反转操作将图片反转并让两个属性指向了同一个内存地址导致了这个调试了一天的问题，上述代码应该修改为  
```
def FlipImg(self,img):
        newImg = numpy.copy(img)
```
进行一次深拷贝，即同样的图像矩阵在两个不同的地址存储了两次  
下文可以帮助进一步理解深/浅拷贝的具体机制：[Numpy中的深拷贝与浅拷贝（视图） -CSDN](https://blog.csdn.net/xxq2002/article/details/123115663)  








QtGui.QImage(uchar * data, int width, int height, int bytesPerLine, Format format)
[CSDN](https://blog.csdn.net/lockhou/article/details/113407322?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-0.pc_relevant_default&spm=1001.2101.3001.4242.1&utm_relevant_index=3)  
QImage img(qImageBuffer, cv_mat.cols, cv_mat.rows, cv_mat.step, QImage::Format_Indexed8);
[CSDN](https://bbs.csdn.net/topics/390918591?page=1)
很多友链：[【Pyqt】opencv显示在label中异常的问题，会出现斜歪的情况解决方案 --CSDN](https://blog.csdn.net/g944468183/article/details/124014785)
[奇怪的QImage转QPixmap方式 --CSDN](https://www.csdn.net/tags/Ntjagg2sNjIzNjEtYmxvZwO0O0OO0O0O.html)

cv2.COLOR_BGR2RGB
Qimage.FORMAT_BGR888
np.uint8
cv2.IMREAD_COLOR
CV_8UC1