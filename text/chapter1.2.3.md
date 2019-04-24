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

![A simple bar](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/A%20simple%20bar.png)

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

* 堆积条形图

&emsp;&emsp;通过提供多组`height`参数，将每组数据生成的图元堆叠到上一组数据的顶端，即可得到堆积条形图。实现代码如下：

```
import matplotlib.pyplot as plt
import numpy as np

x=np.arange(0,10,1)
height1=np.abs(np.random.randn(10))
height2=np.abs(np.random.randn(10))
height3=np.abs(np.random.randn(10))

fig=plt.figure()
ax=fig.add_subplot(111)
ax.bar(x,height=height1) #默认bottom=0,即下底边和y轴重合
ax.bar(x,height=height2,bottom=height1) #下底边和height1的上底边重合
ax.bar(x,height=height3,bottom=height1+height2) #下底边和height1+height2的上底边重合
ax.set_title('A heap bar')
ax.set_xlabel('X data')
ax.set_ylabel('Y data')
```

![A heap bar](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/A%20heap%20bar.png)

* 复合条形图

&emsp;&emsp;复合条形图同样需要提供多组`height`参数，但它改变的是每组条形图的`x`坐标。实现代码如下：

```
import matplotlib.pyplot as plt
import numpy as np

x=np.arange(0,10,1)
height1=np.abs(np.random.randn(10))
height2=np.abs(np.random.randn(10))
height3=np.abs(np.random.randn(10))


fig=plt.figure()
ax=fig.add_subplot(111)
width=0.6 #一组条形图的总宽度
num=3 #条形图的组数
width=width/num #每组条形图的宽度
ax.bar(x-width,height=height1,width=width) #第一组偏左
ax.bar(x,height=height2,width=width) #第二组居中
ax.bar(x+width,height=height3,width=width) #第三组偏右
ax.set_title('A multi bar')
ax.set_xlabel('X data')
ax.set_ylabel('Y data')
```
![A multi bar](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/A%20multi%20bar.png)

## 小结
&emsp;&emsp;条形图的绘制非常灵活。改变`height`与`bottom`以及`x`参数，可以绘制出多变的效果。下面展示一个例子：

```
import matplotlib.pyplot as plt
import numpy as np

x=np.arange(0,10,1)
height1=np.abs(np.random.randn(10))
height2=np.abs(np.random.randn(10))
height3=np.abs(np.random.randn(10))
height4=np.abs(np.random.randn(10))

fig=plt.figure()
ax=fig.add_subplot(111)
width=0.6
num=2
width=width/num
ax.barh(x-width/2,width=height1,height=width,edgecolor='black') #第一组纵坐标偏下，left=0,黑色边框。
ax.barh(x-width/2,width=height2,height=width,left=height1,edgecolor='black') #纵坐标和第一组相同，堆积在第一组上，黑色边框。
ax.barh(x+width/2,width=height3,height=width,left=-height3/2,edgecolor='black') #纵坐标偏上，以x轴为对称轴居中，黑色边框。
ax.barh(x+width/2,width=height4,height=width,left=height3/2,edgecolor='black') #堆积在第三组上，黑色边框。
ax.set_title('A complex bar')
ax.set_xlabel('X data')
ax.set_ylabel('Y data')
```

&emsp;&emsp; **一定要注意`bar()`和`barh()`参数的区别！** 输出结果如下：

![A complex bar](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/A%20complex%20bar.png)
