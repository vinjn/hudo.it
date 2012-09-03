Processing	
==
第八天 **运动的泡泡**
----

想要让昨天写的泡泡动起来，就要给我们的**Bubble()**类添加新的方法- **update（）方法**。如果我们在**draw()**函数里，在调用**render()**方法之前调用了**update()**方法，泡泡的y坐标就会发生变化，泡泡将会被绘制在一个新的坐标位置。
代码如下：

	void update()
	{
		loc.y -= speed;
	}
	
想看到这个动画效果，你需要修改**draw()**里的for循环：

	for (int i = 0; i < bubbles.length; i++) {
    	bubbles<i>.update();
    	bubbles<i>.render();
	}
	
第二个问题是，如果泡泡的坐标跑到屏幕外面去了，我们就根本看不到泡泡，只能看到一个空白的屏幕。这就是我为什么给**Bubble（）**类添加一个**reset**方法。一旦泡泡看不到了，这个方法将重置泡泡的位置，速度和半径。代码如下

	void reset()
	{
    	loc.x = random(width);
    	loc.y = height + 50;
    	speed = random(0.5, 2);
    	radius = random( 5, 10 );
	}

判断泡泡是否能被看到，我们需要添加一个if语句，判断泡泡的y坐标是否小于-50.如果满足条件，我们将对该泡泡调用**reset()**方法。**draw()**函数最后的样子应该是这样：

	for (int i = 0; i < bubbles.length; i++) {
    	bubbles<i>.update();
    	bubbles<i>.render();
    	if ( bubbles<i>.loc.y < -50) {
        	bubbles<i>.reset();
    	}
	}

##下载

点击下面的链接查看完整的源代码，如果您想要查看最后的图形结果，请查看[这个例子的OpenProcessing链接](http://openprocessing.org/visuals/?visualID=28431)。

[Processing Month第八天的文件](http://img.vormplus.be/downloads/processing_month_day_008.zip)