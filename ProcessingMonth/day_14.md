Processing Month
=====
第十四天 **操纵圆形**
----

昨天我们绘制了规则的多边形。想象一下，如果您绘制了一个有360个角点的规则多边形，那么这个多边形相对来说就更接近圆形。或者，使用正弦波和余弦波来操纵半径变化，也许可以得到更有趣的结果，以下是操纵圆形的代码：

	void circleShape( float radius, int numSpikes )
	{
    float amp = random( 0.05, 0.5 );
    beginShape();
    for (int i = 0; i < 360; i++) {
        float a =  (1 + amp * cos(radians(i * numSpikes)));
        float x = cos(radians(i)) * radius * a;
        float y = sin(radians(i)) * radius * a;
        vertex(x, y);
    }
    endShape(CLOSE);
}

我绘制的这些圆圈将会被排布在50像素间隔的网格内。通过for-loops循环嵌套实现。在这个例子里，我试着赋予它们不同的半径，以此生成有趣的结果。

	for (int i = 0; i < 10; i++) {
    for (int j = 0; j < 9; j++) {
        pushMatrix();
        translate( i * 50, j * 50 );
        rotate( random( TWO_PI ));
        circleShape( r, floor(random(3, 6)) );
        popMatrix();    
    }
}

##例子
您可以在[OpenProcessing](http://openprocessing.org/visuals/?visualID=28764)上找到本例子。

![](http://img.vormplus.be/blog/manipulated-circles-10.png)

![](http://img.vormplus.be/blog/manipulated-circles-20.png)

![](http://img.vormplus.be/blog/manipulated-circles-30.png)

![](http://img.vormplus.be/blog/manipulated-circles-50.png)

![](http://img.vormplus.be/blog/manipulated-circles-60.png)

![](http://img.vormplus.be/blog/manipulated-circles-100.png)

##下载

[Processing Month第十四天的文件](http://img.vormplus.be/downloads/processing_month_day_014.zip)