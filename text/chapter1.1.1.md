# 1.1.1&emsp;准备工作
&emsp;&emsp;本文档面向有一定教育程度，对Python语法有初步了解（明白各种数据容器的创建、使用和迭代，能够使用控制流编写基础代码），希望使用Python作图的群体。本文档所述内容绝大部分来自互联网开源教程/课程，文档中引用的代码均标明出处。本文档遵守996.ICU协议。

## 安装Anaconda
&emsp;&emsp;Anaconda是一个开源的Python环境管理器，自带了包括Matplotlib、Numpy、Pandas等诸多第三方库。本文档的全部代码均在安装Anaconda的Windows 10平台上通过测试。请自行去[Anaconda官网](https://www.anaconda.com/)完成安装。如果这一步搞不定的话，恭喜你，你不是本文档的目标人群。

&emsp;&emsp;我们使用Spyder作为编译器。它已经包含在Anaconda中，可以通过Anaconda Navigator->Spyder打开。Spyder界面如下图所示：

![Spyder](https://www.spyder-ide.org/static/images/spyder_website_banner.png)

## 导入Matplotlib
&emsp;&emsp;在Spyder中新建一个.py文档，运行如下代码：

```
import matplotlib
from matplotlib import pyplot as plt
```

&emsp;&emsp;若运行成功，则证明Matplotlib包已被成功导入。
