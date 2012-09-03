Processing Month
=====
第十五天 **圆角矩形**
----

在过去的两年中，“圆角”在网页设计中很火。今天呢，我们就来学习一下怎样在Processing中创建圆角矩形。在这个月的好几个例子里，我们都用到了 **vertex()** 这个命令，今天我们要再学习一个叫做 **bezierVertex()** 的命令来为我们的图形创建圆角。下面是一段完整的从中心创建圆角矩形的代码，其原理与我们使用 **rectMode(CENTER)** 来创建普通矩形的方式是一样的。

	void roundedRect(float w, float h, float r)
	{
    beginShape();
    vertex(  w/2 - r, -h/2 );
    bezierVertex( w/2 - r , -h/2, w/2, -h/2, w/2 , -h/2 + r);
    vertex(  w/2 , h/2 - r );
    bezierVertex( w/2, h/2 , w/2 - r , h/2 , w/2 - r, h/2);
    vertex( -w/2 + r,  h/2 );
    bezierVertex( - w/2, h/2, -w/2, h/2 - r, -w/2 , h/2 - r );
    vertex( -w/2 , -h/2 + r );
    bezierVertex( -w/2, -h/2, -w/2 + r, -h/2, -w/2 + r, -h/2 );
    endShape(CLOSE);
}

把下面的代码放进“draw()”事件中，就可以在窗口中显示圆角矩形了。

	for (int i = 1; i < 20; i++) {
    roundedRect( i * 20, i * 10, i ); 
}

##例子

您可以从[OpenProcessing](http://openprocessing.org/visuals/?visualID=28805)找到这个例子。

![](http://img.vormplus.be/blog/rounded-rectangles.png)

##文档

·[bezierVertex()](http://processing.org/reference/bezierVertex_.html)

##下载

[Processing Month第十五天的文件](http://img.vormplus.be/downloads/processing_month_day_015.zip)