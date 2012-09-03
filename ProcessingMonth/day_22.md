Processing Month
=====
第二十二天 **图案**
----

今天我们来学习绘制图案。我将会使用COLOURlovers API和colorLibs来使我们的图画颜色更有趣。你可以[下载colorLib](http://code.google.com/p/colorlib/)然后将它安装到你的libraries文件夹中。以下是我们需要预先声明的变量：

	ClLovers cl;
	ClLoversTheme[] ctl;

在setup()函数中，我们会创建一个ClLovers物件然后经由关键词搜索COLOURlover网站的调色板，在这个例子里我使用的关键词是“strawberry”（“草莓”）。

	cl = new ClLovers(this);
	ctl = cl.searchForThemes("strawberry");

生成图案的算法很简单。在网格点上绘制上一丛线段就可以了。下面这些参数可供您调整网格的形状、线段的数目和间隔。好好享受这些例子所带给您的乐趣吧！

##例子
下面的图片里，由线段组成的图形是经由搜索关键词"草莓"所获得的，由矩形组成的图形是通过搜索"阳光"获得的。

![](http://img.vormplus.be/blog/pattern-00002.png)

![](http://img.vormplus.be/blog/pattern-00004.png)

![](http://img.vormplus.be/blog/pattern-00006.png)
