Processing Month
=====
第五天-**矩形花朵** 第二部分
----

在前面五天的例子中我们都只画了一个物体，今天我们来学习一下怎么写一个灵活的函数去绘制多个花朵。

一开始我们要在程序末尾定义一个函数，就在draw()函数后面。函数名前面的void关键词表示这个函数没有返回值。

void squareFlower()
{

}

下一步就是要在函数的大括号中建立一些变量。我们需要跟昨天的[矩形花朵第一部分](http://vormplus.be/blog/article/square-flowers-part-1)一样的变量，以及一个额外的变量赋给颜色。

	float x = random(width);
	float y = random(height);
	float steps = floor( random(10, 20) );
	float angle = random( 8, 20 );
	float startSize = random(80, 120);
	color c = color( 128 + random(128), 0, 0);

绘制花朵的算法与昨天的算法相同，不过我们需要添加两个重要函数: **pushMatrix()** 和 **popMatrix()** 。如果我们在 **translate()** 之前不使用 **pushMatrix()** ，那么只有第一朵花会被放置在正确的位置上。一帧只画一朵花是可以的，但若想要绘制一朵花以上就需要使用到 **pushMatrix()** 和 **popMatrix()** 功能。

    stroke( c );
	fill( 0 );
	pushMatrix();
	translate(x, y);
	for ( int i = 0; i < steps; i++ ) {
    rotate( radians( angle * i ) );
    rect( 0, 0, startSize - 5*i, startSize - 5*i);
	}
	popMatrix();

这个功能到这里就写完了，我们可以在 **draw()** 事件中调用这个 **drawFlower()** 事件，这样每一帧会绘制一朵花。如果您想每一帧绘制一个以上的花朵图形，那么您需要多次调用 **drawFlower()** 事件，比如将这个事件放入一个循环中。

##例子
本例文件同样可以在[OpenProcessing](http://www.openprocessing.org/sketch/28338)上找到。

![](http://img.vormplus.be/blog/square-flowers-002-00155.png)

![](http://img.vormplus.be/blog/square-flowers-002-00345.png)

##下载

[ProcessingMonth第六天的文件](http://img.vormplus.be/downloads/processing_month_day_006.zip)
