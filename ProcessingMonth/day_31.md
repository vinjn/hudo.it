Processing Month
=====
第三十一天-使用OpenCV建立互动装置
----

在我的Processing Month系列的最后一天，我想和大家一起学习一下使用Processing建立互动装置方面的内容。我想把我们即将建立的装置叫做“模糊镜”。它的设计概念很简单：把电脑屏幕当做一面电子镜来使用。使用者越靠近屏幕，这面镜子上所显示的图像就越模糊。我们会用到OpenCV数据库中的面部追踪技术，您需要先[下载和安装OpenCV数据库](http://ubaa.net/shared/processing/opencv/)。

##设置OpenCV

在 **setup()** 函数中，我们需要设置OpenCV的追踪目标。我使用OpenCV从我的摄像头中捕捉640×480像素大小的画面。这个尺寸应该足够了。如果您的摄像头支持，您可以使用更高的尺寸，但这会耗费更多的CPU处理时间。我们在 **setup()** 函数中使用的最后一个OpenCV命令是 **cascade()** 。我使用的是标准级联中的( **CASCADE_FRONTALFACE_ALT** )，以此在视频中追踪面部。这个方法同样可以用来加载带有追踪物体描述的xml文件。

	size( 1024, 768 );
	opencv = new OpenCV( this );
	opencv.capture( 640, 480 );
	opencv.cascade( OpenCV.CASCADE_FRONTALFACE_ALT );

##准备图像

下一步是准备面部追踪所需的图像。下面的代码应当是 **draw()** 函数中的第一部分。 **read()** 方法会从摄像头中获取当前的图像应用到我们的装置中。我们还需要使用 **FLIP_HORIZONTAL** 翻转图像得到镜像效果。您也可以调整对比度和亮度获得更好的追踪效果。这些参数需要一个-128到128之间的整数。我使用箭头键来调整这些值。您可以使用OpenCV的 **image()** 命令来显示图像，就像Processing中的image()方法内的第一个参数一样。

	opencv.read();
	opencv.flip( OpenCV.FLIP_HORIZONTAL );
	opencv.contrast( contrastValue );
	opencv.brightness( brightnessValue );
	image( opencv.image(), 0, 0 );

##面部侦测

现在我们的图像已经准备好了，我们需要使用 **detect()** 命令来扫描脸部的正面图像
。以下是代码。我已经导入了java.awt矩形因为 **detect()** 命令会返回一些矩形序列。这些矩形含有位置，宽度和高度，在整个装置中它们会被用作模糊图像的参数。

	Rectangle[] faces = opencv.detect( 1.2, 2, ¬
        OpenCV.HAAR_DO_CANNY_PRUNING, 40, 40 );

因为这个镜子是私人性质的，所以它会被设计成只追踪一个目标，所以这个装置同一时间只与一个人发生互动。第一个if语句是非常重要的，只有当一张脸显示成图像后才能对其进行其他的处理，否则装置会崩溃。我已经将第一个脸部的坐标和宽度映射到Processing草图中。f是一个控制最终图像模糊程度的变量。如果面部图像很小（离镜头远），图像不模糊，如果面部图像大（离镜头近）图像较模糊。我还加入了一个if语句，用作程序的调试，相当于一个由键盘 **d键** 控制的开关。下面的图片显示的就是当某人靠近镜头时所产生的模糊图像。

	if ( faces.length > 0 ) {
	// values needed for debugging
    float x = map( faces[0].x, 0, 640, 0, 1024 );
    float y = map( faces[0].y, 0, 480, 0, 768 );
    float f = map( faces[0].width, 0, 640, 0, 1024 );       
    if ( f <= 200) {
        // no blurring
    } else if ( f > 200 && f <= 300 ) {
        opencv.blur( OpenCV.GAUSSIAN, 11 );    
    } else if ( f > 300 && f <= 400 ) {
        opencv.blur( OpenCV.GAUSSIAN, 31 );    
    } else if ( f > 400 && f <= 500 ) {
        opencv.blur( OpenCV.GAUSSIAN, 51 );   
    } else {
        opencv.blur( OpenCV.GAUSSIAN, 71 );
    }
    image( opencv.image(), 0, 0, width, height );
    if ( DEBUG ) {
        noFill();
        stroke( 255, 0, 0 );
    	rect( x, y, f, f );
    }
}

![](http://img.vormplus.be/blog/blurry-mirror-installation.jpg)

最后，加入一个关闭OpenCV的功能，这样当用户关闭装置时，这个额外的功能会关闭OpenCV。

	public void stop()
	{
    opencv.stop();
    super.stop();
}

##下载
我们已经初步学习了OpenCV，现在，您可以开始着手构建您自己的互动装置了，您可以在[这里](http://img.vormplus.be/downloads/processing_month_day_031.zip)下载到本例子，祝您玩得愉快。
