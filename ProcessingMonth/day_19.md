Processing Month
=====
第十九天 **为激光切割导出PDF文件**
----

今天，我们将学习一下怎样使用PDF 数据库导出激光切割所使用的PDF文件。制作出来的成果不会在屏幕上显示，而是直接在相关文件夹中生成一个PDF文件。作为激光切割的准备，我们需要在文件中定义两种不同的颜色，一个是代表切割的RGB红色，另一个是代表版刻用的RGB黑色。

	color cutColor = color( 255, 0, 0 );
	color engraveColor = color( 0 );

同时，您还需要导入PDF 数据库。**点击菜单栏“sketch”按钮，选择“Import Library”，再点击“PDF Export”**。下面这行命令就被添加进去了。

	import processing.pdf.*;

我们将输出一个一页的PDF文件，所以呢我们的size()命令将会有一些不同，我们需要加入两个参数：加入“PDF”来调用这个功能，然后加入一个文件目录名。我一般会把我的PDF文件存在一个单独的文件夹中。

	size( 800, 800, PDF, "pdf/lines.pdf" );

您可以使用我们先前定义的两种颜色在 **draw()** 函数中任意施为。但是别忘了调用 **stroke()** 命令和 **noFill()** 命令。在 **draw()** 函数的结尾调用 **exit()** 命令是很重要的，它会关闭程序然后保存PDF文件。在一个作品中，我写了一个简短的算法，生成在园内的随机点。这些点是黑色的，这样它们就会被刻出来，圆是红色的，这样，它就会被切下来。你能在相关文件夹中找到PDF文件。

![](http://img.vormplus.be/blog/circle-filled-with-lines-for-lasercutting.png)

在第二个例子中，我将使用第十三天我们一起学习的规则多边形功能。在其中使用 **beginShape()** 和 **endShape()** 功能的时候，加入 **CLOSE** 控制参数是非常重要的，下面第一幅图是一个没有使用 **CLOSE** 的例子，您把这个文件送去激光切割的话，模型甚至都不会从板子上被切下来。第二幅图是正确的做法：

![](http://img.vormplus.be/blog/open-polygon.png)

![](http://img.vormplus.be/blog/closed-polygon.png)

如果您想要玩转印刷和激光切割。那么你可以在完成尺寸设置后加入一个 **textMode(SHAPE)** 命令。这会把我们PDF文件中的字体描出来，另一个问题是我们不能使用 **stroke()** 命令描出字体，而是使用我们早先定义的红色填充它，这样它就能被切出来了。它看起来应该是这样子：

![](http://img.vormplus.be/blog/pdf-typography-with-processing.png)

如果我们想要把它应用到激光切割中，我们还需要使用像Adobe Illustrator那样的工具清理一下PDF文件，这是非常有用的，它能在一个毫米单位的环境中调节文件尺寸，而在Processing里，我们的工作单位是像素。

![](http://img.vormplus.be/blog/cleaning-the-pdf-with-illustrator.png)

##下载
今天的下载包含了所有[三个为激光切割而准备的例子](http://img.vormplus.be/downloads/processing_month_day_019.zip)。