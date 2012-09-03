Processing Month
=====
第二十五天 **圆杆图**
----

今天我们来学习一下数据的可视化设计。我打算试着做一个圆杆图。我不打算使用真正的数据来做这个图，而是使用一个0到100之间的随机数组来代表数据，本例的侧重点是如何将这个图形表述出来。

以下代码可以完整地绘制出这个图形。为了绘制出一个漂亮的图形，您大约需要60个值，当然，30到100个条杆都是可以的。

	class CircularBarChart
	{
    float maxRadius;
    float minRadius;
    float values[];
    float angle;
    CircularBarChart(float[] _values)
    {
        minRadius = 50;
        maxRadius = 200;
        values = _values;
        angle = TWO_PI / float( values.length );
    }
    void renderLines()
    {
        for (int i = 0; i < values.length; i++) {
            float x1 = cos( i * angle ) * ( minRadius / 2 );
            float y1 = sin( i * angle ) * ( minRadius / 2 );
            float r = map(values<i>, 0, 100, minRadius, maxRadius);
            float x2 = cos( i * angle ) * r;
            float y2 = sin( i * angle ) * r;
            line(x1, y1, x2, y2);
        }
    } 
}

##例子

![](http://img.vormplus.be/blog/circular-bar-chart-30.png)

![](http://img.vormplus.be/blog/circular-bar-chart-50.png)

![](http://img.vormplus.be/blog/circular-bar-chart-80.png)

![](http://img.vormplus.be/blog/circular-bar-chart-120.png)

##下载
[Processing Month第二十五天的文件](http://img.vormplus.be/downloads/processing_month_day_025.zip)