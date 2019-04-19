# 1.1.2&emsp;图元介绍
&emsp;&emsp;网上现存的诸多Matplotlib教程里，相当显著的一个缺点是标准混乱。对于一个画折线图的示例，时而用`plt.plot()`，时而又`ax.plot()`，这对于绘制简单的图形并无大碍，但到了绘制三维图形和子图时，免不了令人困扰。因此，本文首先介绍Matplotlib所绘制的图形的构成元素。明确一副图像由哪些元素构成，理解这些元素之间有何关系。然后，再根据这些构成元素简要介绍可视化的一般流程。

## 图形的构成元素

&emsp;&emsp;Matplotlib API包含三层逻辑架构。自底向上分别为后端层，美工层（Artist）和脚本层（pyplot）。后端层中封装了FigureCanvas、Renderer和Event等接口，分别代表绘图表面、绘图动作和绘图事件。**我们的文档一般不涉及这层。** 美工层封装了各种Artist对象，这些对象经过组合构成了最终的图形。**这是我们重点关注的部分。** 脚本层是对Matplotlib的更高级封装，较为易读，面向非专业场合，但对复杂图形的灵活性欠佳。**我们提倡使用面向Artist对象的方式画图**。

&emsp;&emsp;首先，我们对一幅图所包含的Artist对象做简单介绍。

![](https://matplotlib.org/_images/anatomy1.png)

&emsp;&emsp;上图包含文字、坐标轴、曲线、点等内容。整幅图像是一个Figure对象，它也是最大的Artist对象，由诸多次级Artist对象复合得到。Figure对象包含Axes对象，这是我们的绘图命令直接作用的对象。Axes对象则包括图片的各种次级Artist对象，如标题属于Text对象，背景属于Patch对象，线条属于Line2D对象，图例属于Legend对象，x轴和y轴属于Xaxis和Yaxis对象等。它们的关系如下图所示：
![](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/figure3.png)

&emsp;&emsp;关于上文提到的`plt.plot()`和`ax.plot()`，在介绍了图形的构成元素后，不难明白它们的联系。pyplot会检测脚本内部数据结构来查看是否存在当前Figure实例。如果存在，则提取当前Axes对象，并将绘图行为导向Axes.scatter的API调用。若脚本中不存在Figure实例，则会生成一个Figure与Axes，并将它们设为当前值，然后将绘图行为导向Axes.scatter。**我们提倡在绘图前先预设Axes对象，这是绘制复杂图像的良好习惯。**

* 不指定Axes对象，让pyplot自动创建。

```
fig1=plt.figure()
plt.scatter(x,y)
plt.title('Scatter')
plt.show()
```
* 指定Axes对象

```
fig2=plt.figure()
ax=fig2.add_subplot(111)
ax.scatter(x,y)
ax.set_title('Scatter')
plt.show()
```

&emsp;&emsp;两段代码对单张图像的绘制效果完全一致（见下图）。但在绘制多子图时，就需要为每个子图分配Axes对象。所以再次强调：**提倡在绘图前先预设Axes对象！**

![](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/2019-04-19%20(4).png)

&emsp;&emsp;数据可视化的过程，就是将经过组织的数据根据某种绘制方法转换为Artist对象，并按照合适的顺序组织这些Artist对象的过程。我们在下一节讨论这个话题。
## 可视化一般流程

&emsp;&emsp;根据上面介绍的Artist对象关系，自顶向下，即可得到数据可视化的一般流程：

![](http://upload-images.jianshu.io/upload_images/13614507-841afa8cc90fde22.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/699)

