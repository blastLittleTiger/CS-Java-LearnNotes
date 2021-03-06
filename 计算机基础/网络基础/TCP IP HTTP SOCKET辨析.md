### TCP IP HTTP SOCKET辨析
***
#### 概述
首先放图

![o_TCP,IP,HTTP,SOCKET区别和联系2](../../images/o_TCP,IP,HTTP,SOCKET区别和联系2.png)

通过上图，我们可以回顾TCP/IP体系的5（4）层架构，与**各个层运行的主要的协议**，从上面看还不太清楚，可以看下面，**HTTP**对应**应用层**，**TCP**对应**传输层**，HTTP高于TCP，这就说明**TCP协议是为HTTP协议服务的**，实际上也是如此，++TCP协议为HTTP提供可靠交付的协议++，**需要说明的是HTTP协议是基于TCP服务的，<font color=red>没有基于UDP的版本</font>**。
进一步，还可以看出的是，IP协议对应于网络层，在TCP协议之下，因此**IP协议为TCP协议提供服务**，++IP协议本身是一个**尽力**交付的协议，但是*配合ICMP(英特网报文控制协议)，就可以提供可靠交付的服务*。

![o_TCP,IP,HTTP,SOCKET区别和联系](../../images/o_TCP,IP,HTTP,SOCKET区别和联系.png)

但是上图没有体现出Socket的概念，其实，**Socket是一个抽象出来的概念**，其目的在于方便我们对于TCP或者UPD传输协议的使用，**是面向于编程语言层级**的，位于**应用层**（HTTP）与**传输层**（TCP）“之间”，++<font color=red>方便编程的使用</font>++。

###### 各自阐述
<font color=Blue>HTTP是**轿车**，提供了封装或者显示数据的具体形式；Socket是**车轮**，提供了通信的驱动力，TCP是**发动机**，提供了原始的通信能力</font>。

| 名称 | 层次 | 作用 | 备注 |
|--------|--------|--------|--------|
|  HTTP      |   应用层     |  超文本传输协议（HTTP，HyperText Transfer Protocol)是运行于应用层的网络协议。所有的**WWW**文件都必须遵守这个标准。 |   我们在传输数据时，可以只使用（传输层）TCP/IP协议，但是那样的话，如 果没有应用层，便无法识别数据内容，如果想要使传输的数据有意义，则必须使用到应用层协议，应用层协议有很多，比如HTTP、FTP、TELNET等，也 可以自己定义应用层协议。WEB使用HTTP协议作应用层协议，以封装HTTP文本信息，然后使用TCP/IP做传输层协议将它发到网络上     |
|  SOCKET    |   \-\-\-    |  **Socket是应用层与TCP/IP协议族通信的中间软件抽象层**，它是一组接口。在设计模式中，Socket其实就是一个门面模式，++它把复杂的TCP/IP协议族隐藏在Socket接口后面++，对用户来说，*一组简单的接口就是全部，让Socket去组织数据，以符合指定的协议*。      |   **虚拟概念**，Socket是对TCP/IP协议的封装，**Socket本身并不是协议，而是一个调用接口（API）**，++通过Socket，我们才能使用TCP/IP协议++。 实际上，**Socket跟TCP/IP协议没有必然的联系，Socket编程接口在设计的时候，就希望也能适应各种的网络协议**。    |
|  TCP      |  传输层      |  TCP（Transmission Control Protocol） 传输控制协议是一种面向连接的、可靠的、基于字节流的传输层通信协议 |  TCP/UDP协议通过设计++封装形成了以供编程使用的*Socket套接字++     |
|  UDP      |  传输层      |  提供无连接的尽力交付的服务    |  **和HTTP协议无关**      |
|  IP       |  网络层      |  为TCP和UDP协议提供服务      |  不可靠的，但是其服务的TCP是可靠服务，通过ICMP等协议来完成可靠性的保证  |


ref:
1.[Http协议与TCP协议简单理解](http://blog.csdn.net/sundacheng1989/article/details/28239711), 2.[Http协议与TCP协议简单理解后续](http://blog.csdn.net/sundacheng1989/article/details/52437128), 3.[简单理解Socket及TCP/IP、Http、Socket的区别](http://blog.csdn.net/jenminzhang/article/details/47017741), 4.[TCP,IP,HTTP,SOCKET区别和联系](http://www.cnblogs.com/lavenderone/archive/2011/10/14/2212523.html), 5.[写给那些让我糊里糊涂的HTTP、TCP、UDP、Socket](http://blog.csdn.net/xijiaohuangcao/article/details/6105623), 6.[http、TCP/IP协议与socket之间的区别](http://www.cnblogs.com/iOS-mt/p/4264675.html), 7.[TCP/IP、Http、Socket的区别?](https://www.zhihu.com/question/39541968), 8.[通信协议——Http、TCP、UDP](2867720), 9.[TCP，HTTP，SOCKET概念区分](http://blog.csdn.net/zhongguomin/article/details/6052319), 10.[TCP/IP、Http的区别](http://www.cnblogs.com/renyuan/archive/2013/01/19/2867720.html), 11.[网络层、传输层、应用层、端口通信协议编程接口 - http，socket，tcp/ip 网络传输与通讯知识总结](http://www.cnblogs.com/dev-xp/p/5714833.html)