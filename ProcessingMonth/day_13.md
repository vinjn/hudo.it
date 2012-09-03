Processing Month
=====
第十三天-**规则多边形**
----

今天我们要写一个灵活的函数来画规则多边形。Processing只提供基本的图形内置画法，例如圆形、长方形、三角形，所以要是如果手边有一些随取随用的函数用来画一些其他图形会方便很多。这个画规则多边形的函数看起来跟我们[第四天 星星](http://vormplus.be/blog/article/processing-month-day-4-stars)用的算法很像。

下面的代码就是一个绘制多边形的完整函数。它包括一个浮点数表示的半径，整型数表示的点的个数。

	void regularPolygon( float radius, int numPoints )
	{
    float angle = TWO_PI / numPoints;
    beginShape();
    for (int i = 0; i < numPoints; i++) {
        float x = cos( i * angle ) * radius;
        float y = sin( i * angle ) * radius;
        vertex( x, y );
    }
    endShape(CLOSE); 
}

如果你想在屏幕上画一个多边形，必须先用  **translate()** 函数。这个函数使我们能从图形中心开始绘制图形。我用了一个for-loop循环来画多个多边形，由此可见该小函数功能之强大。

	translate( width/2, height/2 );
	for (int i = 0; i < 18; i++) {
    regularPolygon( 10 + i * 10, 3 + i );
}

##例子
您可以在[OpenProcessing](http://www.openprocessing.org/visuals/?visualID=28713)上找到本例。

![](http://img.vormplus.be/blog/regular-polygons.png)

##下载
[Processing Month第十三天的文件](http://img.vormplus.be/downloads/processing_month_day_013.zip)