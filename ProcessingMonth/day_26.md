Processing Month
=====
第二十六天 **数据可视化**
----

在今天的学习中，我们要同时用到两个之前做过的例子，试着把它们结合起来：1.数据可视化 2.使用PDF文件进行激光切割。以下是一个我写的创建这个有形状的数据集的算法。

![](http://img.vormplus.be/blog/data-visualisation-finished-lasercut-001.jpg)

![](http://img.vormplus.be/blog/data-visualisation-finished-lasercut-002.jpg)

绘制这个多边形的算法与昨天的绘制条杆的算法有些相似。我们会用到beginShape()命令在每次循环内绘制两个顶点。

	void renderPolygon()
	{
    float closeX = 0;
    float closeY = 0;
    beginShape();
    for (int i = 0; i < values.length; i++) {
        float r = map(values<i>, 0, 100, minRadius, maxRadius);
        if ( i == 0 ) {
            closeX = cos(i * angle) * r;
            closeY = sin(i * angle) * r;
        }
        float x1 = cos(i * angle) * r;
        float y1 = sin(i * angle) * r;
        float x2 = cos((i + 1) * angle) * r;
        float y2 = sin((i + 1) * angle) * r;
        vertex(x1, y1);
        vertex(x2, y2);
    }
    endShape(CLOSE);
    ellipse( 0, 0, minRadius, minRadius );
    ellipse( minRadius/2 + 5, 0, 4, 4 );
}

我们会用到圆圈的最大半径和最小半径变量，然后使用lerp()命令定位各个圆圈半径。各个圆之间的间隔是间距的10%，这样切完以后，每个条杆都会清晰可见。

	void renderCircles()
	{
    float diff = maxRadius - minRadius;
    for (int i = 0; i < 10; i++) {
        float r = lerp( minRadius, maxRadius, i / 10.0 ) * 2;
        noFill();
        ellipse( 0, 0, r, r );
    }
    ellipse( 0, 0, maxRadius * 2, maxRadius * 2 );
}

输出的结果如下图所示。如果您结合使用一些PDF输出技术的算法，一定能制作出更漂亮的数据图形。

![](http://img.vormplus.be/blog/data-visualisation-for-lasercutting.png)

##下载
[Processing Month第二十六天的文件](http://img.vormplus.be/downloads/processing_month_day_026.zip)