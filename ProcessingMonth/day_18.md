Processing Month
=====
第十八天 **完成游戏**
----

今天我们将要为我们的小游戏“躲避小行星”收尾。我将改变一下绘制的方式，我们绘制一个代表爆炸效果的[星星](http://vormplus.be/blog/article/processing-month-day-4-stars)来描述飞船被小行星撞击时的情况。为了侦测我们的飞船是否被小行星撞击到，我们将使用到 **collide()** 和 **circleLineInterset()** 命令。我不会细述这两个命令的细节，我自[Casey Reas](http://www.openprocessing.org/visuals/?visualID=8009)那里引述了 **circleLineInterset()** ，Casey Reas自[Pauls Bourke](http://local.wasp.uwa.edu.au/~pbourke/geometry/sphereline/raysphere.c)那里引述了这个功能。

我们还需要写一段检查游戏有没有结束的代码，这里有一些关于游戏结构的伪代码：

	if ( life > 0 ) {
	// draw asteroids	
	// draw spaceship
	// if ship was hit by asteroid, draw star and reset game
	} else {
	// draw "game over" to the screen
}

当我们的飞船被小行星撞击时，我们画一个动态的星形来表示爆炸效果。当爆炸扩展到它自己的最大范围时，我们需要重设所有的小行星和飞船，去掉一条命，并且停住整个游戏一秒钟。

	void resetAfterHit()
	{
    for (Asteroid a : asteroids ) {
        a.reset();
    }
    spaceShip.reset();
    life--;
    delay(1000);
}

当玩家输掉整个游戏，玩家可以通过按空格键重玩游戏。我们需要重设小行星、飞船并且将生命值和计分器调回初值。

	void resetGame()
	{
    for (Asteroid a : asteroids ) {
        a.reset();
    }
    spaceShip.reset();
    life = 3;
    score = 0;
}

##小练习
·试着为游戏加入这样一个个功能：玩家每获得1000分奖励一条额外的命。（提示：使用“ % ”运算符）

·制作一个高分榜，以文本文档方式显示出来。

##下载
[Processing Month第十八天的文件](http://img.vormplus.be/downloads/processing_month_day_018.zip)