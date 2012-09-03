Processing Month
=====
第二十四天 **客户端/服务器** 第二部分
----

在“使用processing进行客户端/服务器编程”的第二部分，我们将尝试构建客户端小程序。您创建的客户端物件需要同服务器保持相同的端口数。如果你在同一台机器上运行客户端文件，您会用到这个ip地址：127.0.0.1，如果在其他电脑上运行，你需要使用运行该文件的电脑ip地址。

	client = new Client( this, "127.0.0.1", 5000 );

我们还需要把字节数组转换成整数。你可以在功能标签中找到它。

	int byteArrayToInt(byte[] bytes) {
    int bits = 0;
    int counter = 0;
    for (int i = 3; i >= 0; i--) {
        bits |= ((int) bytes[counter] & 0xff) << (i * 8);
        counter++;
    }
    return bits;
}

最后，我们需要读取小程序在 **clients.readBytesUntil()** 命令中传递给字节缓冲器的数据，并且从其中获取x和y坐标，使用这些坐标在屏幕上画圆和线。

	if ( client.available() > 0 ) 
	{
    int byteCount = client.readBytesUntil( interesting, byteBuffer );
    byte[] xb = new byte[4];
    for (int i = 0; i < 4; i++) {
        xb<i> = byteBuffer<i>;
    }
    byte[] yb = new byte[4];
    for (int i = 0; i < 4; i++) {
        yb<i> = byteBuffer[i+4];
    }
    int x = byteArrayToInt( xb );
    int y = byteArrayToInt( yb );
    line( x, y, prevX, prevY );
    ellipse( x, y, 10, 10 );
    prevX = x;
    prevY = y;
}

##截屏
我创建了一个截屏，这样您就可以看到这个小程序是怎么运作的了，您可以在[Vimeo](http://vimeo.com/24178953)上找到这个操作视频。

##下载
[Processing Month第二十四天的文件（其中已经包括了第二十三天的服务器文件）](http://img.vormplus.be/downloads/processing_month_day_024.zip)
