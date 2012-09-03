Processing Month
=====
第五天 **矩形花朵** 第一部分
----

今天我们要学习一下如何通过叠加多个矩形来绘制一朵花。您将会用到 **translate()** 和 **rotate（）** 这两个新的方法。

第一步，使用 **rectMode(CENTER)** 来使你的矩形以中心点方法绘制。 **rect()** 函数的默认方法是从矩形左上角的角点开始绘制的。

在开始绘制图形之前，我们需要定义一些变量。角度变量用来转动方形。要注意角度是以度数为单位的。steps变量是组成花朵的正方形个数。flowerSize变量是指最大的那个正方形的大小，stepSize是用来控制正方形每次减小的程度。

	float angle = 6;
	int   steps = 50;
	float flowerSize = 150;
	float stepSize = 3;

我们想在屏幕中心画这朵花，所以我们用 **translate(width/2，height/2)** 把坐标原点移至窗口中心。我们需要这样做所以我们才能将所有正方形的中心定在窗口中心然后转动它们。 **rotate()** 函数是以0点为中心转动的。如果我们不用translate()函数而是使用 **rect(width/2，height/2，flowerSize，flowerSize)** 画正方形的话，我们就会得到完全不同的结果。

![](http://img.vormplus.be/blog/no-translation.png)

所以这个算法要这样来，使用 **radians()** 函数需要把角度制的角度转换为弧度制，而 **rotate()** 函数需要用弧度制。

	translate( width/2, height/2 );
	for ( int i = 0; i < steps; i++ ) {
    rotate( radians( angle * i ) );
    rect( 0, 0, flowerSize - (stepSize * i), flowerSize - (stepSize * i) );
}

明天我们会学习如何创建一个可以绘制多个不同花朵的方法。

##例子
这个例子同样也可以在[OpenProcessing](http://openprocessing.org/visuals/?visualID=28291)上找到。

![](http://img.vormplus.be/blog/square-flowers-001-00001.png)

![](http://img.vormplus.be/blog/square-flowers-001-00002.png)

![](http://img.vormplus.be/blog/square-flowers-001-00003.png)

##文档


- [rectMode()](http://processing.org/reference/rectMode_.html)

- [translate()](http://processing.org/reference/translate_.html)

- [rotate()](http://processing.org/reference/rotate_.html)

- [radians() ](http://processing.org/reference/radians_.html)

##下载

[Processing Month第五天的文件](http://img.vormplus.be/downloads/processing_month_day_005.zip)