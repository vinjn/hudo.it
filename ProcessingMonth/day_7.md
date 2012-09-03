Processing Month
=====
第七天 **泡泡**
----

在屏幕上一次绘制多个物件一定是一件很爽快的事，但是如果我们想控制这些物件的其中一个，使它们运动起来，我们必须找到其他的方法。今天我们将进入OOP的世界:面向对象编程。

如果我们已经读过目前为止的所有文章，并跟着例子做了一遍，其实你已经使用了一些面向对象编程的东西。在第一天，我们使用了PVector类，来跟踪点的x,y坐标。今天我们要建立自己的类，用这个类在屏幕上绘制一个泡泡。在编辑器里新建一个标签，命名为Bubble，输入以下代码：

	class Bubble
	{
    Bubble()
    {
    }
}

Bubble()方法被称为构造函数，被用来建立一个Bubble对象，并初始化一些我们需要的变量。那些变量必须在Bubble()之前声明。如果我们在构造函数里声明了这些变量，那么我们将无法在我们的写的类的其他方法中调用这些变量。所以，我们要在函数构造器之前声明这些量：

	PVector loc;
	float   speed;
	float   radius;
搞定了上面之后，我们可以给这些变量赋值。添加如下代码：

	loc = new PVector( random(width), random(height) );
	speed = random(0.5, 2);
	radius = random( 5, 10 );

我们将添加一个在屏幕上绘制泡泡的方法，我么可以测试一下这个类库。我经常给屏幕绘制的方法命名为 **render()** ，因为他们只在屏幕上画东西，并没有返回值，所以我们要在方法前加上一个关键字 **void** 。

	void render()
	{
    	stroke(59, 173, 224);
		fill(59, 173, 224, 64);
    	for (int i = 1; i < 3; i++) {
        ellipse( loc.x, loc.y, i * radius * 2, i * radius * 2 ); 
    }
}

render()方法在屏幕上画了两个圆圈。请注意，在for循环里，i是从1开始的，因为如果是从0开始，那么将会画出一个直径是0的圆，这样的圆是不可见的。想要在屏幕上绘制一个泡泡，我们需要在 **setup()** 函数里新建一个Bubble类型的对象，然后调用这个对象的 **render()** 方法。

	Bubble b = new Bubble();
	b.render();

你的结果应该和下图类似。代码见**processing_month_day_007_001 ** 

![](http://img.vormplus.be/blog/one-bubble.png)

要想绘制很多泡泡，你需要创建一个容纳多个泡泡物件的数组，就像我们在第一天额例子中所创建的PVector物件数组。若您想要往这个数组中加入泡泡物件，可以在draw()函数中使用一个for-loop循环。如下所示：

	for (int i = 0; i < bubbles.length; i++) {
    bubbles<i>.render();
}

你的结果应该和下图类似。代码见processing_month_day_007_002  

![](http://img.vormplus.be/blog/oop-50-bubbles.png)

明天，我们将会在类中添加一些新的方法，让我们的泡泡动起来。因此，我们需要往泡泡类库中添加一个速度变量，那么，今天的文件我就不往OpenProcessing上传了，我将会在明天的例子里加上完整版本的上传地址。

##下载

[Processing Month第七天的文件](http://img.vormplus.be/downloads/processing_month_day_007.zip)
