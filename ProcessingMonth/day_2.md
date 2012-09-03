Processing Month
====
第二天 **连接点** 第二部分
----

今天的例子和昨天的类似，只不过我们将使用随机点代替固定点，连接点的时候也将采用不同的方式。如果两点之间的距离小于某一个我们定义的数，我们就把这两个点连接起来。并且将连线的透明度与两点距离相关联，距离越大，连线就越透明。


我们用 **dist()** 函数来计算两个点之间的距离。前两个参数是第一个点的x坐标和y坐标。第三，第四个参数是另外一个点的x坐标和y坐标。返回值为一个float类型的数值，代表两点之间的距离。如果距离小于255，我们就在这两点之间连线。


	float dst = dist( points<i>.x, points<i>.y, points[j].x,points[j].y );
	if ( dst < 255 ) {
   		stroke( 255, 255 - dst );
    	line( points<i>.x, points<i>.y, points[j].x, points[j].y );
	}
	
	
画完这些细线之后，我们稍微放大点的体量，这样会让图像更好看。以下这些代码将加入到第一个for-loop循环的结尾、内部循环之后。


	stroke( 255 );
	strokeWeight(4);
	point( points<i>.x, points<i>.y );

##成果

![](http://img.vormplus.be/blog/random-connections-16.png)

![](http://img.vormplus.be/blog/random-connections-20.png)

![](http://img.vormplus.be/blog/random-connections-28.png)

![](http://img.vormplus.be/blog/random-connections-40.png)

##文档
下面的链接是我所使用的几个功能的processing说明文档，如果您需要一些关于该功能的额外信息，这些文档会很有帮助。

·[dist()](http://processing.org/reference/dist_.html)

·[strokeWeight()](http://processing.org/reference/strokeWeight_.html)

##下载

[Processing Month 第二天的文件](http://img.vormplus.be/downloads/processing_month_day_002.zip)