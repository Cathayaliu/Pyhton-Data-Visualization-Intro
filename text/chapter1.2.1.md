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

&emsp;&emsp;它会生成如下图所示的散点图。

![A simple scatter](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/A%20simple%20scatter.png)

&emsp;&emsp;注意，我使用了`numpy`的`random`模块随机生成了x坐标和y坐标的数据。这意味着每次运行代码得到的图像不会相同，不要惊慌，这是正常现象。

## 可调参数

&emsp;&emsp;你可能注意到了，上面的图片着实有些……乏味。所幸，`scatter()`提供了相当多的可选参数，可以让你拥有相当大的发挥空间。接下来讲几个比较常用的可选参数。

* s

&emsp;&emsp;`s`大概是`size`的缩写。顾名思义，它可以改变散点的尺寸。你既可以传入一个固定值，比如`s=40`，让图中所有的点大小相同；也可以传入一个长度与x/y数据集相同的数组，为每个点指定尺寸。比如，假如你的数据是`x=[2,3,4,5]`,`y=[5,6,7,8]`,你可以传入`s=[10,20,13,9]`。试试看！

* color

&emsp;&emsp;显然这个参数可以改变散点的颜色。你可以传入一个颜色描述字符串，比如`color='skyblue'`，或是一个三元RGB组，比如`color=(0.5,0.8,0.7)`。当然，也可以是16进制的颜色标号，比如`color=#AABBCC`。你可以在下图找到更多颜色描述字符串的信息。

![颜色字符串](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/color_str.png)

* marker

&emsp;&emsp;这个参数用来改变点的形状。除了圆形之外，还有很多其他形状。你可以传入`marker='+'`将散点由圆形变成十字。关于marker所能提供的全部形状，官网有如下说明：

```
markers = {'.': 'point', ',': 'pixel', 'o': 'circle', 'v': 'triangle_down', '^': 'triangle_up', '<': 'triangle_left', '>': 'triangle_right', '1': 'tri_down', '2': 'tri_up', '3': 'tri_left', '4': 'tri_right', '8': 'octagon', 's': 'square', 'p': 'pentagon', '*': 'star', 'h': 'hexagon1', 'H': 'hexagon2', '+': 'plus', 'x': 'x', 'D': 'diamond', 'd': 'thin_diamond', '|': 'vline', '_': 'hline', 'P': 'plus_filled', 'X': 'x_filled', 0: 'tickleft', 1: 'tickright', 2: 'tickup', 3: 'tickdown', 4: 'caretleft', 5: 'caretright', 6: 'caretup', 7: 'caretdown', 8: 'caretleftbase', 9: 'caretrightbase', 10: 'caretupbase', 11: 'caretdownbase', 'None': 'nothing', None: 'nothing', ' ': 'nothing', '': 'nothing'}
```

* alpha

&emsp;&emsp;这个参数用来改变散点的透明度。`alpha=0`代表这个点完全透明。`alpha=1`代表完全不透明。你可以传入介于0和1之间的值。

## 小结
&emsp;&emsp;最后，我们再来画张图，总结一下上面的内容。绘制代码如下：

```
#引入模块
import matplotlib.pyplot as plt
import numpy as np

x=np.random.randn(100)
y=np.random.randn(100)

fig=plt.figure()
ax=fig.add_subplot(111)
ax.scatter(x,y,s=30*(x*x+y*y),color='skyblue',alpha=0.9) #画图，点的大小等于其距离原点的距离乘以30，颜色为天蓝色，透明度为0.9
ax.scatter(x,y,s=30*(x*x+y*y),color='blue',alpha=0.5,marker='*') #画图，大小同上，颜色为蓝色，透明度为0.5，形状为星形
ax.set_title('A beautiful scatter')
ax.set_xlabel('X data')
ax.set_ylabel('Y data')
```
&emsp;&emsp;最终效果图：

![A beautiful scatter](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/A%20beautiful%20scatter.png)

