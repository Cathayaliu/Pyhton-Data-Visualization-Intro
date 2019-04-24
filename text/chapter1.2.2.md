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
&emsp;&emsp;在数据量较少的时候，折线图会有非常强硬的“转折”（这就是它名字的由来吧www）。如果想要获得平滑的曲线，一个直观的想法就是增加数据量。通过`scipy`模块的`interpolate`函数，我们可以在两个数据点之间插入根据数学方法生成的数值，从而使曲线平滑化。

&emsp;&emsp;使用插值法绘制折线图的代码如下：

```
import matplotlib.pyplot as plt
import numpy as np
import scipy #这个模块用来实现插值

x=np.arange(0,20,1)
y=np.random.randn(20)

x_new=np.arange(0,19,0.1) #注意这里的范围从（0，20）变为（0，19）
func=scipy.interpolate.interp1d(x, y, kind='cubic') #使用x和y的数据，创造一个插值函数，插值类型为3阶B样条曲线
y_new=func(x_new) #使用插值函数，传入x_new的数据，得到插值后的y_new数据

fig=plt.figure()
ax=fig.add_subplot(111)
ax.plot(x_new,y_new) #使用新数据画图
ax.set_title('A smooth plot')
ax.set_xlabel('X data')
ax.set_ylabel('Y data')
```
&emsp;&emsp;未经插值和插值后的效果见下图：

![A hard plot](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/A%20hard%20plot.png)

![A smooth plot](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/A%20smooth%20plot.png)

&emsp;&emsp;上面的代码有几个点需要说明一下。首先`x_new`的范围从(0,20)变成了(0,19)的原因是，`x`数组中包含的元素为`[0,1,2,...,18,19]`而不是`[0,1,2,...,19,20]`。我们使用`x`和`y`数组的数据创建插值函数，因此这个函数只能处理(0,19)范围内的数据，传入的`x_new`范围自然是(0,19)。其次，创建插值函数语句的`kind=cubic`是插值类型的一种。还有最邻近插值、线性插值等方法。如果对这个部分感兴趣，请自行google，毕竟这不是数学教材。

## 小结
&emsp;&emsp;小结部分依然是综合运用上面介绍的知识画图，代码如下：

```import matplotlib.pyplot as plt
import numpy as np
import scipy

x=np.arange(0,20,1)
y=np.random.randn(20)

#平滑化部分
x_new=np.arange(0,19,0.1)
func=scipy.interpolate.interp1d(x, y, kind='cubic')
y_new=func(x_new)

fig=plt.figure()
ax=fig.add_subplot(111)
ax.plot(x,y,lw=2.5,color='violet') #原始数据线，线宽2.5，颜色为紫色
ax.plot(x_new,y_new,lw=2.5,color='slategray',ls='-.',alpha=0.5) #平滑化曲线，线宽2.5，颜色为铅灰，线形点划线，透明度0.5
ax.set_title('A complex plot')
ax.set_xlabel('X data')
ax.set_ylabel('Y data')

```

&emsp;&emsp;最终效果图：

![](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/A%20complex%20plot.png)
