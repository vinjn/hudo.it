Processing Month
=====
第二十七天 **网格基础**
----

今天我们来学习如何使用 **beginShape()** 中的 **QUAD_STRIP** 和 **TRIANGLE_STRIP** 模式绘制图形。这里有一篇[使用Processing绘制3D图形](http://vormplus.be/blog/article/drawing-3d-shapes-with-processing)的教程，希望它会对您有帮助。今天的第一个例子是绘制一组矩形组成的条杆。

	beginShape(QUAD_STRIP);
	for (int i = 0; i < 11; i++) {
    vertex( i * 40, 0 );
    vertex( i * 40, 60 );
	}
endShape();

![](http://img.vormplus.be/blog/quadstrip.png)

第二个例子使用 **TRIANGLE_STRIP** ，生成由三角形组成的条杆。

	beginShape(TRIANGLE_STRIP);
	for (int i = 0; i < 11; i++) {
    vertex( i * 40, 0 );
    vertex( i * 40, 60 );
	}
endShape();

![](http://img.vormplus.be/blog/trianglestrip.png)

如果我们想要绘制一个网格，我们会用到嵌套循环。代码和第一个例子相似。计算每一个顶点的y坐标，然后再嵌入另一个循环。注意最外层的循环增长到10就结束，而不是11，因为如果那么做，我们就会得到一个11×10的矩形。

![](http://img.vormplus.be/blog/quadstrip-grid.png)

如果您想要绘制三角形网格，那么用 **TRIANGLE_STRIP** 模式代替 **QUAD_STRIP**  就可以了，生成的结果如下：

![](http://img.vormplus.be/blog/trianglestrip-grid.png)

##下载
[Processing Month第二十七天的文件 ](http://img.vormplus.be/downloads/processing_month_day_027.zip)