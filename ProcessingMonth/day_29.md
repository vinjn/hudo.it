Processing Month
=====
第二十九天 **扭曲的3D网格**
----

今天我们来学习一下将[昨天构建的网格](http://vormplus.be/blog/article/processing-month-day-28-distorted-grids)转换为3维的网格。首先，为 **size()** 命令增加第三个参数，若您已经导入了OpenGL数据库，那么您就可以用 **OPENGL** 来代替第三个参数，在这里我们选择使用 **P3D** 渲染模式，当我们生成PVector阵列时，我们需要一个第三参数来构建PVector。它将会用作空间点的z坐标。我使用的是-20到20的随机数。在draw()函数中，您需要将这个z坐标加入 **vertex()** 命令中。

##例子

3D中的网格如下图所示。我使用 **lights()** 命令为网格加入一些阴影效果。

![](http://img.vormplus.be/blog/3d-grid-001.png)

![](http://img.vormplus.be/blog/3d-grid-002.png)

![](http://img.vormplus.be/blog/3d-grid-003.png)

![](http://img.vormplus.be/blog/3d-grid-004.png)

##下载
[Processing Month第二十九天的文件](http://img.vormplus.be/downloads/processing_month_day_029.zip)