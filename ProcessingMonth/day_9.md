Processing Month
=====
第九天 **圆形的像素**
----

今天，我们来学习一下怎样在processing中处理图像及如何调用颜色值来生成一些有趣的结果。首先，我们要做到的是找到一副图像,然后重新定义它的尺寸以使其与Processing窗口尺寸相符合。我使用的照片来自我的照片博客“[La Vie En Ville](http://www.lavieenville.be/)”,鼠标拖拽着重新定义过尺寸的图像放进编辑窗口中，这样图像文件会自动添加到当前processing文件保存目录下的**data**文件夹中。在 **setup()** 命令之前，我们需要声明一个类型为PImage的变量，然后我们就可以通过这个变量来加载“data”文件夹中的图像及调用图像中的像素了。我们可以通过使用 **loadImage()** 命令将图像放入processing存储后台中，然后使用 **image()** 命令将这个图像显示出来。

	PImage img;
	void setup()
	{
    size( 450, 400 );
    img = loadImage("smoking.jpg");
    image( img, 0, 0 );
}

单纯地将图像原原本本显示出来稍显无趣。在第一个例子里，我将使用 **brightness()** 命令来获取单个像素的（明亮度的）值，建立一个圆圈的网格（即用规则排布的圆圈填满整个窗口），然后根据获取到的像素（明亮度的）值来对相应位置的圆圈进行灰度填充。因为我们并不需要每个像素的值，所以我把for-loops循环中的计数间隔增大到10.

	translate( 5, 5 );
	for (int i = 0; i < width; i+=10) {
    for (int j = 0; j < height; j+=10) {
        float c = brightness( img.get( i, j ) );
        fill( c );
        ellipse( i, j, 10, 10 );
    }
}

这些代码可以在文件夹**processing_month_009_001 **中找到。原始照片和生成结果看起来应该是这样：

![](http://img.vormplus.be/blog/fire-extinguisher.jpg)

![](http://img.vormplus.be/blog/fire-extinguisher-circular-pixels.png)

或者，我们也可以把获取到的明亮度的值赋给圆圈的直径。这个 **brightness()** 命令会返回一个范围在0至255之间的值。如果我们将这个值（等比例）映射到一个0至10的范围内，我们就可以把这个新值用作我们圆圈的新的直径，在这里我们可以使用 **map()** 命令。

	for (int i = 0; i < width; i+=10) {
    for (int j = 0; j < height; j+=10) {
        float c = brightness( img.get( i, j ) );
        float r = map( c, 0, 255, 0, 10);
        fill( 255 );
        ellipse( i, j, r, r ); 
    }
}

这些代码可以在文件夹 **processing_month_009_002** 中找到。原始文件和生成结果看起来应该像这样：

![](http://img.vormplus.be/blog/superhero.jpg)

![](http://img.vormplus.be/blog/superhero-circular-pixels.png)

我们也可以结合上面两个算法，获取像素颜色后将其赋值给圆圈的描边，就像下面的算法所演示的那样。其中的可能性是无穷的。运用您的想象力去创造更多的算法吧。您可能会使用三角形或星形，也许会用到 **red()** 命令， **green()** 命令或者 **blue()** 命令来创造更有趣的图像。

	for (int i = 0; i < width; i+=10) {
    for (int j = 0; j < height; j+=10) {
        int   c = img.get( i, j );
        float b = brightness( c );
        fill( b );
        stroke( c );
        float r = map( b, 0, 255, 0, 10);
        ellipse( i, j, r, r ); 
    }
}

这些代码可以在文件夹 **processing_month_009_003** 中找到。原始文件和生成结果看起来应该是这样:

![](http://img.vormplus.be/blog/ceiling.jpg)

![](http://img.vormplus.be/blog/ceiling-circular-pixels.png)

##文档

·[PImage](http://processing.org/reference/PImage.html)

·[loadImage()](http://processing.org/reference/loadImage_.html)

·[image()](http://processing.org/reference/image_.html)

·[get()](http://processing.org/reference/get_.html)

·[brightness()](http://processing.org/reference/brightness_.html)

·[map()](http://processing.org/reference/map_.html)

##下载

[Processing Month第九天的文件](http://img.vormplus.be/downloads/processing_month_day_009.zip)