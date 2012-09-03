Processing Month
=====
第二十八天 **扭曲网格**
----

今天，我们来学习如何扭曲我们昨天绘制的网格。为了获得这个效果，我们需要稍稍调整一下我们的算法。我们需要一个多维向量 **PVector** 数组来追踪网格点。我们会计算法向量点，然后使用 **random()** 函数使他们稍稍偏离网格。下面是代码：

	for (int j = 0; j < 11; j++) {
    for (int i = 0; i < 11; i++) {
         vertices<i>[j] = new PVector( i*40 + random(-10, 10),
                                       j*40 + random(-10, 10) );
    }
}

同样的，绘制网格的代码也和昨天的算法有些不同。在这个例子里，我们不计算点的位置，我们通过前面我们已经设置好的PVector阵列获得他们。

	for (int j = 0; j < 10; j ++) {
    beginShape(QUAD_STRIP);
    for (int i = 0; i < 11; i++) {
        vertex( vertices<i>[j].x, vertices<i>[j].y );
        vertex( vertices<i>[j+1].x, vertices<i>[j+1].y );
    }
    endShape();
}

##例子
如果我们使用 **QUAD_STRIP** 和 **TRIANGLE_STRIP** 绘制网格，图形看起来应该是这样。

![](http://img.vormplus.be/blog/quadstrip-grid-distort.png)

![](http://img.vormplus.be/blog/trianglestrip-grid-distort.png)

##下载
[Processing Month第二十八天的文件](http://img.vormplus.be/downloads/processing_month_day_028.zip)