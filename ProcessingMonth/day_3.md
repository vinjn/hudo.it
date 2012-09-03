Processing Month
=====
第三天 **三角形网格**
----

第三天是关于绘制三角形的，但我们并不是直接使用 **triangle()** 函数，而是画点和线，我们会限制线条，只绘制基于规则三角形的网格。为了使它更有趣，稍后我们会加入一些动画效果。

图画的起始点位于窗口中央，因为我们要使线条动起来，所以我们需要跟踪当前点和前一个点的位置，把它们用线连接起来。我们还需要一个半径来计算新的点。我们最好在程序的开头就定义好这些变量。

 	float radius = 20;
	float x, y;
	float prevX, prevY;

下一步我们需要给这些变量赋值。起始点设在窗口的中心，所以我们将 **width** 和 **height** 除以2，然后分别赋值给x和y。width和height是内置系统变量，可以通过size()来赋值，并可以随时调用。

	x = width / 2;
	y = height / 2;    
	prevX = x;
	prevY = y;

接着，我们该编写 **draw()** 函数了。计算下一个点我们要用到 **cos()** 和 **sin()** ，它俩是我们在第一天用过的功能。因为我们要做的三角形是规则的，所以线条只需要在六个特定的方向移动，算法很简单。

1.三个角的度数之和是180度或者说是PI

2.我们做的是等边三角形，所以每个角是180/3=60度

3.一个圆是360度或者TWO_PI，如果我们用60去除，得到6个方向的线

4.这些线的角度分别是0,60,120,180,240和300

我想让电脑去决定画哪个方向，所以我用随机数来计算方向。但是，random()功能所产生的结果是float值，而我想要的结果是0,1,2,3,4,5之间的整数，所以我加了一个 **floor()** 功能，它会达到取整的效果。

	float angle = (TWO_PI / 6) * floor( random( 6 ));
	x += cos( angle ) * radius;
	y += sin( angle ) * radius;

这样每次 **draw()** 函数每调用一次点就会移动到网格上的新位置。下一步我们需要在当前点和前一个点之间画线。我们还需要在 **draw()** 的末尾将前一点替换为当前点，否则在第一帧之后就不会有动态了。

	stroke( 255, 64 );
	strokeWeight( 1 );
	line( x, y, prevX, prevY );
	strokeWeight( 3 );
	point( x, y );
	// update prevX and prevY with the new values
	prevX = x;
	prevY = y;

如果你运行程序会发现线条不断往窗口外扩散回不来了。我们需要在确定x和y值之后实现一个算法来确保线条留在屏幕内。我们要检查新的x是不是小于0或者超出了宽度范围。如果是这样，我们要把x和y值还原成之前的值，这样线条就不会超出窗口范围了，y值也做相同处理。

	if ( x < 0 || x > width ) {
    x = prevX;
    y = prevY;
}

	if ( y < 0 || y > height) {
    x = prevX;
    y = prevY;
}

为了使我们的图画更有趣，我们给背景加一个淡出效果，这样那些线会像蛇一样移动。加入一个开关功能使用键盘按键来控制这个效果。为了达到这样的目的，我们需要在程序前加一个boolean变量。

Boolean fade = true;

下面的代码应当放在 **draw()** 函数的最前面，我们要先判断fade值是不是为真。如果为真，if语句中的代码会在最上层画一个透明的长方形。

	if (fade) {
    noStroke();
    fill( 0, 4 );
    rect( 0, 0, width, height );
}

想要关闭淡出效果，我们要用到keyPressed()这个方法，它会在每次键盘有按键动作时被调用。如果用户按了**f** 键，系统就切换一次fade的真假值。

	void keyPressed(){

    if (key == 'f') {
        fade = !fade;
    }
}

运行程序后你就能看到之前的线条都慢慢淡出背景，试一下f键关闭或启用淡出效果。

##例子
![](http://img.vormplus.be/blog/triangle-grid-001.png)

![](http://img.vormplus.be/blog/triangle-grid-002.png)

![](http://img.vormplus.be/blog/triangle-grid-003.png)

![](http://img.vormplus.be/blog/triangle-grid-004.png)

##下载
[Processing Month 第三天的文件](http://img.vormplus.be/downloads/processing_month_day_003.zip)