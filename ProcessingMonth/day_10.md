Processing Month
=====
第十天 **绘画** 第一部分
----

在接下来的三天，我们将会涉猎一些程序化的绘图。今天主要的内容是要学习一下绘图的用户介入。我们会使用鼠标的移动来模拟笔刷。为了使它更有趣一些，我们加入一个使笔刷在某个半径范围内跳动的算法。我们使用HSB模式代替RGB模式，这样我们就可以给图形赋予一个由色相值产生的随机颜色了。

首先我们声明一些变量。一个代表色相值的浮点数，一个代表当前半径的浮点数，一个代表最小半径的浮点数，一个代表最大半径的浮点数以及一个控制笔刷增长或收缩的布尔值。

	float h;
	float r = 15;
	float minRadius = 10;
	float maxRadius = 20;
	boolean grow = false;

为了把颜色模式从RGB切换到HSB，您需要使用到 **colorMode()** 方法。我会将三个所需的参数设为100，色相范围设置到360。我们也可以使用processing内置工具栏tools中的Color Selector来帮助我们选取颜色。

	colorMode( HSB, 360, 100, 100, 100 );
	h = random(360);

下面我们就要开始进行draw()函数的编写了。根据我们在 **setup()** 中获得的色相值来为图形填充和图形描边设置随机的透明度。最后，加上画圆的命令，等着看好戏吧！

	fill( h, random(100), random(100), 50 );
	stroke( h, random(100), random(100), 70 );
	ellipse(mouseX, mouseY, r * 2, r * 2);

最后，我们为笔刷的跳动算法加一个运动范围，当笔刷增长到最大半径时，将grow布尔值变为假，当笔刷收缩到最小半径时，将grow布尔值变为真。

	if ( grow ) {
    r++;
    if (r > maxRadius) {
        grow = false;
    } 
	} else {
    r--;
    if (r < minRadius) {
        grow = true;
    }
}

![](http://img.vormplus.be/blog/painting-001-pink.png)

![](http://img.vormplus.be/blog/painting-001-yellow.png)

##文档

·[colorMode()](http://processing.org/reference/colorMode_.html)


##下载

您可以在[OpenProcessing](http://www.openprocessing.org/visuals/?visualID=28547)上找到这个例子。如果您想要调试一下代码，您可以在这里下载[Processing Month第十天的文件](http://img.vormplus.be/downloads/processing_month_day_010.zip)