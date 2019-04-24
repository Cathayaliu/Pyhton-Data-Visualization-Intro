# 1.2.2&emsp;折线图

## 图片介绍
&emsp;&emsp;折线图通常用来可以某种数值随另一种数值（通常是时间）的变化趋势，也经常被用于比较几种数值指标的变化情况。与散点图不同的是，使用折线图时我们更关注某个变量的“变化趋势”，而散点图通常着眼于两个变量之间的“相关性”。
## 绘制方法
&emsp;&emsp;Matplotlib使用`plot()`函数绘制折线图。最基础的折线图绘制代码为：

```
import matplotlib.pyplot as plt
import numpy as np

x=np.arange(0,20,1) #生成0-20，间隔为1的均匀数组，作为x坐标
y=np.random.randn(20) 随机生成20个浮点数，作为y坐标

fig=plt.figure()
ax=fig.add_subplot(111)
ax.plot(x,y) #绘制折线图的命令
ax.set_title('A simple plot')
ax.set_xlabel('X data')
ax.set_ylabel('Y data')
```

![A simple plot](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/A%20simple%20plot.png)

&emsp;&emsp;上文说到，折线图反应的是某种数值的变化趋势。因此在生成x坐标数据的时候，没有使用随机生成，而是用`np.arange()`生成了等差数列。这样，y坐标数据的变化趋势就被较好地反映出来了。

## 可调参数
&emsp;&emsp;在 **1.2.1&emsp;散点图** 中，已经对一些可调参数做了介绍。这些参数的大部分（除了`s`）在折线图绘制中依然适用。接下来介绍两个折线图特有的可调参数。

* linewidth

&emsp;&emsp;顾名思义，这个参数决定折线图的线宽。你可以传入一个浮点数，例如`linewidth=2.1`，或简写为`lw=2.1`。

* linestyle

&emsp;&emsp;该参数决定折线图的线条风格。可以传入一个字符串，例如`linestyle=':'`，或简写为`ls=':'`。可以传入的字符串见下表：

|字符串|对应线条风格|
|-----|-----------|
|'-'|实线|
|'--'|破折线|
|'-.'|点划线|
|':'|虚线|

## 使用插值法绘制平滑曲线



## 小结
