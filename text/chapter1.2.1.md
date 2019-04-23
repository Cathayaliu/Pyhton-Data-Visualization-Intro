# 1.2.1&emsp;散点图

## 图片介绍
&emsp;&emsp;散点图将两组数据（分别提供x轴和y轴的坐标信息）显示为平面上的一组点。数据值由点在图表中的位置表示，考察坐标点的分布，可以判断两变量之间是否存在某种关联或总结坐标点的分布模式。若存在多组数据，则不同组的数据由图表中的不同标记表示。
## 绘制方法
&emsp;&emsp;Matplotlib使用`scatter()`函数绘制散点图。最基础的散点图绘制代码为：

```
#引入模块，matplotlib.plt用来画图，numpy用来生成画图所需的数据。
import matplotlib.pyplot as plt
import numpy as np

x=np.random.randn(1000) #随机生成1000个数据，作为x坐标
y=np.random.randn(1000) #随机生成1000个数据，作为y坐标

fig=plt.figure() #创建Figure对象
ax=fig.add_subplot(111) #创建Axis对象
ax.scatter(x,y) #在Axis对象上绘制散点图
ax.set_title('A simple scatter') #为Axis对象添加标题
ax.set_xlabel('X data') #为Axis对象添加x轴标签
ax.set_ylabel('Y data') #为Axis对象添加y轴标签
```

它会生成如下图所示的散点图。

![A simple scatter](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/A%20simple%20scatter.png)

注意，我使用了`numpy`的`random`模块随机生成了x坐标和y坐标的数据。这意味着每次运行代码得到的图像不会相同，不要惊慌，这是正常现象。

## 可调参数
