# 1.1.2&emsp;图元介绍
&emsp;&emsp;网上现存的诸多Matplotlib教程里，相当显著的一个缺点是标准混乱。对于一个画折线图的示例，时而用`plt.plot()`，时而又`ax.plot()`，这对于绘制简单的图形并无大碍，但到了绘制三维图形和子图时，免不了令人困扰。因此，本文首先介绍Matplotlib所绘制的图形的构成元素。明确一副图像由哪些元素构成，理解这些元素之间有何关系。然后，再根据这些构成元素简要介绍可视化的一般流程。

## 图形的构成元素

&emsp;&emsp;Matplotlib API包含三层逻辑架构。自底向上分别为后端层，美工层（Artist）和脚本层（pyplot）。后端层中封装了FigureCanvas、Renderer和Event等接口，分别代表绘图表面、绘图动作和绘图事件。**我们的文档一般不涉及这层。** 美工层封装了各种Artist对象，这些对象经过组合构成了最终的图形。**这是我们重点关注的部分。** 脚本层是对Matplotlib的更高级封装，较为易读，面向非专业场合，但对复杂图形的灵活性欠佳。**我们提倡使用面向Artist对象的方式画图**。

&emsp;&emsp;首先，我们对一幅图所包含的Artist对象做简单介绍。

![](https://matplotlib.org/_images/anatomy1.png)

&emsp;&emsp;上图包含文字、坐标轴、曲线、点等内容。整幅图像是一个Figure对象，它也是最大的Artist对象，由诸多次级Artist对象复合得到。Figure对象包含Axes对象，这是我们的绘图命令直接作用的对象。Axes对象则包括图片的各种次级Artist对象，如标题属于Text对象，背景属于Patch对象，线条属于Line2D对象，图例属于Legend对象，x轴和y轴属于Xaxis和Yaxis对象等。它们的关系如下图所示：
![](https://github.com/Cathayaliu/Pyhton-Data-Visualization-Intro/blob/master/picture/chapter%201/figure3.png)

&emsp;&emsp;数据可视化的过程，就是将经过组织的数据根据某种绘制方法转换为Artist对象，并按照合适的顺序组织这些Artist对象的过程。我们在下一节讨论这个话题。
## 可视化一般流程
