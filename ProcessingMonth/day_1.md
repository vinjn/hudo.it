Processing Month
=====
第一天 **连接点** 第一部分
----

这篇文章中，我们来看一下如何计算一个圆周上的点的坐标，并将他们连接起来。我们将用灵活的方式来实现基于6个点和18个点的图像

##计算
要计算这些点的坐标，必须知道圆上的点数量和圆的半径。本例中，我们将画12个点。

	int numPoint = 12;
	float radius = 150;

下一步，我们来算一下每个点之间的角度。众所周知一个整圆的角度是360度或2π弧度，所以用360度除以圆上的点数，就得到两点之间的角度。例子中使用了弧度而不是角度，是因为 **cos()** 和 **sin()** 函数的形参是弧度数，不是角度数。Processing中有一些关于圆和半圆的常量， **TWO_PI** 就代表了常量PI*2。（这里的PVector其实是类型，代表这一个点）

	float	angle = TWO_PI / numPoint;
	for(int i=0 ; i<numberPoints;i++){
		float x = cos(angle * i ) * radius;
		float y = sin(angle * i ) * radius;
		point[i] = new PVector(x,y );
	}
	
我把计算的部分放在了setup()里面，把结果存在了PVector数组里，这样我们就不用在draw函数里一遍又一遍的计算点的x、y坐标。我还用了一个for循环，用来计算每个点的坐标，**angle*i** 会在每个循环中计算出一个点的坐标。

##绘制

接下来我们说一下，如何将圆上的点两两连线，我们需要用一个嵌套for循环，来遍历数组中的每一个点。if语句用来比较i和j的数字，如果他们不相等，电脑就在这两个点之间画一条线。如果i和j相等，说明是同一个点，那么就不用画线了。

	for (int i = 0; i < numPoints; i++) {
    	for (int j = 0; j < numPoints; j++) {
        	if ( j != i ) {
           	    line( points<i>.x, points<i>.y,points[j].x,points[j].y );        
        	}
   		 }
	}

##成果
![](http://img.vormplus.be/blog/circle-connections-6.png)

![](http://img.vormplus.be/blog/circle-connections-12.png)

![](http://img.vormplus.be/blog/circle-connections-18.png)

![](http://img.vormplus.be/blog/circle-connections-24.png)

##文档
下面的链接是我所使用的几个功能的processing说明文档，如果您需要一些关于该功能的额外信息，这些文档会很有帮助。

· [cos()](http://processing.org/reference/cos_.html)

· [sin()](http://processing.org/reference/sin_.html)

· [TWO_PI](http://processing.org/reference/TWO_PI.html)

##下载

[Processing Month 第一天的文件](http://img.vormplus.be/downloads/processing_month_day_001.zip)