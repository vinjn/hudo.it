Processing
====
Day11 **绘画** 第二部分
----
我们今天用的笔刷的算法和昨天的[绘图 第一部分](http://vormplus.be/blog/article/processing-month-day-10-painting-part-1)一样。但是我们今天不用HSB模式，就像[第九天的课程 圆形的像素](http://vormplus.be/blog/article/processing-month-day-9-circular-pixels)中提到的，我们尝试着从图像中提取颜色。

从图像中取颜色，存在一个问题，提取的颜色没有透明度，所以我写了一个函数，用它返回带有透明度的颜色值。注意一下，我写的这个函数，没有以void开始。这个函数以 **color** 关键字开始，是因为函数返回一个color类型的值。 这个函数通过一个叫bit shifting的技术*其实就是移位和位操作*得到颜色的红、绿、蓝分量。代码读起来挺复杂的，但事实上，比使用 **red()** ， **green()** 和 **blue()** 方法要快一些。

	color getTransparentColor( color c, float a )
	{
    	int r = (c >> 16) & 0xff;
    	int g = (c >> 8) & 0xff;
    	int b = c & 0xff;	
    	return color(r, g, b, a);
	}
	
你可以通过传入第一个参数来设置当前鼠标位置的颜色值，第二个参数的范围为0~255，0代表全透明，255代表不透明。

	color c = getTransparentColor( img.get( mouseX, mouseY ), 64 );
	fill( c );
	ellipse(mouseX, mouseY, r * 2, r * 2);

##例子
以下是原始图片和两个根据算法获得的效果图。

![](http://img.vormplus.be/blog/milky.jpg)

![](http://img.vormplus.be/blog/painting-002-3149.jpg)

![](http://img.vormplus.be/blog/painting-002-4619.jpg)

##文档

·[right shift](http://processing.org/reference/rightshift.html)

·[red()](http://processing.org/reference/red_.html)

·[green()](http://processing.org/reference/green_.html)

·[blue()](http://processing.org/reference/blue_.html)

##下载
[Processing Month第十一天的文件](http://img.vormplus.be/downloads/processing_month_day_011.zip)
	
	