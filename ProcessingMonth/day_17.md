Processing Month
=====
第十七天 **坠落的小行星**
----

今天我们的任务是让行星动起来并且为游戏加入一个得分板.小行星类跟[Day 8](http://vormplus.be/blog/article/processing-month-day-8-animating-bubbles)的气泡类很相似.主要不同点在于，第一，当行星消失在窗口边缘时，系统应当更新得分板的分数。第二，我们的小行星持续降落,而第八天中的气泡持续上升。

	{
    PVector location;
    float   speed;
    float   radius;
    Asteroid()
    {
        location = new PVector( random( width ), -20 );
        speed = random( 1, 2 );
        radius = random( 10, 20 );
    }
    void update()
    {
        location.y += speed;
        if (location.y >= height + radius) {
            reset();
            score++;
         }
    }
    void render()
    {
        fill(0);
        stroke(255, 0, 0);
        pushMatrix();
        translate( location.x, location.y );
        ellipse( 0, 0, radius * 2, radius * 2 );
        popMatrix();
    }
    void reset()
    {
         location.x = random(width);
         location.y = -20;
         speed = random( 1, 2 );
         radius = random( 10, 20 );
    }
	}

还有一个不同点是，我们用数组列表（ArrayList）来存储Asteroid对象.这个比第八天的数组（Array）要灵活.你可以随便在数组列表添加或移除对象.如果我们像这样定义数组列表,我们就可以用一个很简单干净的for循环来更新对象并把它们绘制在屏幕上。

	ArrayList<Asteroid> asteroids;

注意我们用 **add()** 方法来往数组列表里面添加对象.这段代码应该放在 **setup()** 函数里面.

	asteroids = new ArrayList<Asteroid>();
	for (int i = 0; i < 10; i++) {
   	asteroids.add( new Asteroid() );
	}

把行星画到屏幕,把这段代码加入draw(),在绘制飞船之前，欣赏一下我们的代码吧，看看我们的for循环是多么的简练啊!

	for (Asteroid a : asteroids ) {
    a.update();
    a.render();   
	}

我们还需要声明一个用来记录得分的变量。我们用一个整型数并设置它的初值为0.要显示计分板,我们需要用 **text()** 函数。计分板应显示在最上层,所以我们在 **draw()** 的末尾写它的代码.使用nf()函数来格式化这个分数显示,使它保持在5位.

	fill(255);
	text("SCORE: " + nf(score, 5), 225, 20 );


##文档
·[ArrayList](http://processing.org/reference/ArrayList.html)

·[nf()](http://processing.org/reference/nf_.html)

##下载
[Processing Month第十七天的文件](http://img.vormplus.be/downloads/processing_month_day_017.zip)