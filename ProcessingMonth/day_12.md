Processing Month
=====
第十二天 **绘图** 第三部分
----

在昨天的绘图中，我们学习了如何使用图像像素的颜色来创建笔刷，今天的任务有些类似，不同的是我们将会创建自引导的绘图系统。建立一个笔刷的类，这样就可以生成多个笔刷为我们绘图了。

在这个笔刷类中，我们需要一个PVector表述笔刷的位置，我们还需要使用浮点小数来定义笔刷尺寸，旋转角度和笔刷的颜色。在类的构造函数中，我们将PVector的坐标，笔刷尺寸和旋转角度都设置为随机值。

	Brush()
	{
    loc = new PVector( random(width), random(height) );
    r   = random(5, 15);
    rot = random( TWO_PI );
}

我们使用布朗运动来移动笔刷。为笔刷的位置坐标加入一个在x轴和y轴上皆为-2到2的随机值。哦对了，还需要将笔刷的位置坐标限制在一定范围内，这样笔刷就不会跑出屏幕一去不复返了。

	void update()
	{
	loc.x += random(-2, 2);
	loc.y += random(-2, 2);       
	loc.x = constrain( loc.x, 0, width );
	loc.y = constrain( loc.y, 0, height );
	c = getTransparentColor( img.get( floor(loc.x), floor(loc.y) ), 64);
	rot += 0.01;
}

我使用的是矩形的笔刷，这样笔刷的旋转现象可以更明显，代码如下：

	void render()
	{
    fill( c );
    pushMatrix();
    translate( loc.x, loc.y );
    rotate( rot );
    stroke( 0, 64 );
    rect( 0, 0, r * 2, r * 2 );
    popMatrix();
}

想要在屏幕上绘制笔刷，你会使用到一些与[第八天-运动的泡泡](http://vormplus.be/blog/article/processing-month-day-8-animating-bubbles)中所演示的相似技术。

##小练习

使用第四天我们编写的[星星](http://vormplus.be/blog/article/processing-month-day-4-stars)来做一个有趣的笔刷吧。

##例子

![](http://img.vormplus.be/blog/wires.jpg)

![](http://img.vormplus.be/blog/painting-003-21919.jpg)

![](http://img.vormplus.be/blog/painting-003-37024.jpg)

##文档
·[constrain()](http://processing.org/reference/constrain_.html)

##下载

[Processing Month第十二天的文件](http://img.vormplus.be/downloads/processing_month_day_012.zip)