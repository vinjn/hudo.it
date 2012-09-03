Processing Month
=====
第三十天 **粒子系统**
----

今天，我们使用[第二天](http://vormplus.be/blog/article/processing-month-day-2-connecting-points-part-2)所编写的算法来生成一个简单的粒子系统。每一个粒子都有一个坐标、一个速度和一个颜色属性。当粒子运动至一个超出屏幕的位置时，这个粒子灭亡，同时另一个新的粒子出现。这是一个创建持续运动系统的简单方法。当粒子之间靠的足够近时，它们之间会连起一条线。我使用 **lerp()** 命令来计算连线点的位置，用 **lerpColor()** 来为每个连线点着色。

##粒子
我使用video数据库渲染得到了动画效果。这个高清影片同样可以在[Vimeo](http://vimeo.com/24419668)上找到。

##下载
[Processing Month第三十天的文件](http://img.vormplus.be/downloads/processing_month_day_030.zip)