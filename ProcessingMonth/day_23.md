Processing
===
第二十三天 **客户端/服务器** 第一部分
---

今天和明天，我们将学习计算机之间通信的“黑暗艺术”。我们使用Processing自带的[Network](http://processing.org/reference/libraries/net/index.html)库。今天来创建一个服务端程序发送鼠标的位置给客户端，明天会继续编写客户端的程序。你需要在 **setup()** 中开启一个服务器，服务器的端口号要选的稍微大一点。我在例子中用的是5000，作为端口号。

	server = new Server( this, 5000 );
	
我们保持这个程序尽可能的简单。 **draw()** 中唯一的代码是下面一行。 server.write（）方法是Network库中的一部分，取得鼠标位置的  **getMousePositionAsByteArray()** 这个函数，我们需要自己写：

	server.write( getMousePositionAsByteArray() );
	
想要和客户端进行通信，我们需要将信息以字节数组的形式发送。mouseX和mouseY变量都是整型变量（在内存中占用32bit），所以我们要将每个整数转换为4个字节的byte。

	byte[] intToByteArray(int number) {
    	byte[] result = new byte[4];
    	for (int i = 0; i < 4; i++) {
       		int offset = (result.length - 1 - i) * 8;
        	result<i> = (byte) ((number >>> offset) & 0xff);
    	}
    	return result;
	}

我们需要创建一个数组，用来发送鼠标位置给客户端。这个数组中含有x轴位置，y轴位置，还有一个字节，用来作为客户端和服务器端同步的标识。以下函数用来创建一个9字节的数组，包含鼠标的位置和一个单独的“标识”字节。

	byte[] getMousePositionAsByteArray()
	{
    	byte[] x = intToByteArray( mouseX );
    	byte[] y = intToByteArray( mouseY );    
    	byte[] b = new byte[9];
    	for (int i = 0; i < 4; i++) {
        	b<i> = x<i>;
    	}
    	for (int i = 4; i < 8; i++) {
        	b<i> = y[i-4];
    	}
    	b[8] = 10; // separator byte
    	return b;
	}

##下载
[Processing Month第二十三天的文件](http://img.vormplus.be/downloads/processing_month_day_023.zip)
