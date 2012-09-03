Processing
=====
第四天 **星星**
-----
今天我们来看一下如何使用processing绘制更复杂的图形。我们会用到 **beginShape()** , **endShape()** 和 **vertex()** 这三个函数在屏幕上画一个星星。最开始我们声明一些变量，用来计算星星的点：内半径，外半径，尖角的个数和一个用来保存点坐标的数组。需要注意的是，这个数组的元素个数是 **2*numSpikes** （尖角数量的两倍），因为其中既有内半径上的点又有外半径上的点。

	float innerRadius = 70;
	float outerRadius = 180;
	int numSpikes = 5;
	PVector[] points = new PVector[ numSpikes * 2 ];
	
接下来的事情是计算绘制星星所需的所有点。我们需要确保这些点的顺序，偶数点分布在外圈，奇数点在内圈。要做到这个奇偶分布，我们需要使用取模运算符。如果i%2的余数是0，那么这个点就是偶数点，分布在外圈。

    float angle = TWO_PI / points.length;
	for ( int i = 0; i < points.length; i++ ) {
    	float x, y;
    	if ( i % 2 == 0 ) {
        	x = cos( angle * i ) * outerRadius;
        	y = sin( angle * i ) * outerRadius;
    	} else {
        	x = cos( angle * i ) * innerRadius;
        	y = sin( angle * i ) * innerRadius;
    	}
    		points<i> = new PVector( x, y );
	}

想把星星绘制到屏幕上，我们使用 **beginShape()** 和 **endShape()** 函数，利用我们计算的点来绘制。 我们在这两个函数中间，利用一个for循环来遍历所有的数组，给每个点生成一个对应的Vertex。确保你调用 **endShape()** 函数时，参数为 **CLOSE** ，否则的话，图形就不会封闭。

	translate( width/2, height/2 );

	beginShape();

	for (int i = 0; i < points.length; i++) {

    vertex( points<i>.x, points<i>.y );
}
	
	endShape(CLOSE);

##例子
![](http://img.vormplus.be/blog/star-5.png)

![](http://img.vormplus.be/blog/star-6.png)

![](http://img.vormplus.be/blog/star-12.png)

![](http://img.vormplus.be/blog/star-24.png)

##OpenProcessing
我把这个例子的文件发布到网站“OpenProcessing”上，你可以通过以下链接找到它：[Stars，OpenProcessing](http://openprocessing.org/portal/?userID=11331)。

##文档
·[beginShape()](http://processing.org/reference/beginShape_.html)

·[endShape()](http://processing.org/reference/endShape_.html)

·[vertex()](http://processing.org/reference/vertex_.html)

##下载
[Processing Month第四天的文件](http://img.vormplus.be/downloads/processing_month_day_004.zip)