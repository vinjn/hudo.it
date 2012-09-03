Processing Month
=====
第十六天 **建造一个宇宙飞船**
----

在接下来的几天里，我们将学习使用基本的键盘互动来设计一个游戏。今天我们要绘制一个酷酷的宇宙飞船并且使用按键来移动它。我们将用一个三角形来描述宇宙飞船，就像街机经典游戏 小行星 中的飞船一样。下面的代码是我们飞船的完整类库。我们用一个PVector来描述位置，用三个点来组成三角形。也许我们可以只使用位置然后直接绘制三角形，但是那些附加的点是非常有用的，尤其是在之后几天我们进行碰撞侦测的图形设计时。

	class SpaceShip
	{
    PVector location;
    PVector point1;
    PVector point2;
    PVector point3;
    SpaceShip()
    {
        location = new PVector( width/2, 360 );
        point1 = new PVector( location.x , location.y - 20 );
        point2 = new PVector( location.x + 10, location.y + 20 );
        point3 = new PVector( location.x - 10, location.y + 20 ); 
    }
    void update(float x)
    {
        location.x += x;
        location.x = constrain( location.x, 15, width - 15 );
        point1.set( location.x , location.y - 20, 0 );
        point2.set( location.x + 10, location.y + 20, 0 );
        point3.set( location.x - 10, location.y + 20, 0 );
    }
    void render()
    {
        fill(0);
        stroke(255);        
        triangle( point1.x, point1.y, point2.x, point2.y, point3.x, point3.y );
    }
}

为了移动飞船，我们要用到键盘上的左右方向键。他们是Processing内置的调用命令，我们只需要分辨输入的按键是左还是右，以此来更新飞船的位置。方法如下：

	void keyPressed()
	{
    if (key == CODED) {
        if (keyCode == LEFT) {
            spaceShip.update( -10 );
        }
        if (keyCode == RIGHT) {
            spaceShip.update( 10 );
        }
    }
}

为了把飞船画进屏幕中，我们还需要为draw()事件添加一个 **noSmooth()** 方法。这会使我们的飞船看起来更像是80年代早期的产物，那个时候可没有抗锯齿这种东西。

	void draw()
	{
    background(0);
    noSmooth();
    spaceShip.render();
}

##宇宙飞船
我们的宇宙飞船看起来应该就像下图显示的一样，如果你正确完全地完成了以上步骤，那么这个飞船能够响应你的左右按键经行移动。

![](http://img.vormplus.be/blog/spaceship.png)

##下载

[Processing Month第十六天的文件](http://img.vormplus.be/downloads/processing_month_day_016.zip)