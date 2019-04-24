# 1.2.3&emsp;条形图
## 图片介绍
&emsp;&emsp;条形图使用宽度相同的矩形色块的高度或长度来表示数据的统计特征。条形图可以横置或纵置，纵置时也称为柱形图。条形图将数值与图元的几何特征直接关联，非常直观，常用于不同类别的数据比较，有时也被用来展示数据的演变趋势。
## 绘制方法
&emsp;&emsp;Matplotlib使用`bar()`函数绘制条形图。最基础的条形图绘制代码为：

```
import matplotlib.pyplot as plt
import numpy as np

x=np.arange(0,10,1)
y=np.abs(np.random.randn(10)) #此处取绝对值是为了确保条形图均在y轴上方。若y数组中有负值，则该项在y轴下方

fig=plt.figure()
ax=fig.add_subplot(111)
ax.bar(x,y) #绘制条形图的代码
ax.set_title('A simple bar')
ax.set_xlabel('X data')
ax.set_ylabel('Y data')
```

&emsp;&emsp;绘制结果如下：

![A simple bar]()

&emsp;&emsp;将`bar()`改为`barh()`，即可得到横置条形图。请读者自行尝试。

## 可调参数
&emsp;&emsp;不同于散点图和折线图，条形图的基本图元是矩形。因此，其参数也与散点图和折线图有较大的差别。现介绍几种常用参数，若读者想深入了解，可阅读Matplotlib中关于条形图的[官方文档](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.bar.html)

* x

&emsp;&emsp;这个数组用来决定绘制矩形的位置，一般情况下，可以理解为条形所在的横坐标。

* height

&emsp;&emsp;这个数组用来描述每个条形的高度（或长度），其长度与`x`相同。在`barh()`函数中，这个参数被`width`替代。

* bottom

&emsp;&emsp;这个数组用来描述每个条形底部所在的坐标。在默认情形下，'bottom=0'，条形的上缘坐标等于它的高度。你可以传入一个浮点数，统一改变所有条形的底部位置，也可以传入一个长度等于条形个数的数组，为每个条形图元设置底部坐标。在`barh()`函数中，这个参数被`left`替代。

* edgecolor

&emsp;&emsp;顾名思义，这个参数控制矩形边框的颜色。其使用方式与`color`相同。另外，条形图中也有`linewidth`参数，它被用来控制矩形边框的粗细。

## 几种绘制技巧




## 小结
