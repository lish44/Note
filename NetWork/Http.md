# Http
--------
### 访问流程
其实可以当做一条指令，可以看做分两个部分，“Opt”和“object”
+ opt 就是http自带的方法，要进行啥子样的操作
+ object就是要操作的对象，其实就是URL指定的那个文件

发送请求就是用http自带的方法，比如Get。然后携带URL参数，发送给服务器。然后服务器根据发过来的请求，返回 __响应消息__ 其实就是一些数据并且附带状态码。比如404就是没找到资源，500表示服务器错误，403表示不能浏览目录访问失败。
![pic](https://raw.githubusercontent.com/lish44/pic/main/res/202205162329001.png)

如果是纯字就访问结束。如果有图片
+ 浏览器会在显示文字的时候搜索这些标签
+ 然后把这些位置空间预留出来（所以元素会写高和宽）
+ 然后再次访问Web服务器，按照图片指定的路径去拿
+ 然后返回并显示到预留的空间中

书上的例子
![pic](https://raw.githubusercontent.com/lish44/pic/main/res/202205162330859.png)
![pic](https://raw.githubusercontent.com/lish44/pic/main/res/202205162331802.png)
![pic](https://raw.githubusercontent.com/lish44/pic/main/res/202205162331412.png)

<font color=#f4433c>1 条请求消息中只能写 1 个 URI。如果需要获取多个文件，必须 对每个文件单独发送 1 条请求。</font> 


### 格式
![pic](https://raw.githubusercontent.com/lish44/pic/main/res/202205162330604.png)
[消息头和消息体](https://blog.csdn.net/destiny1507/article/details/81701106) 


### Http主要方法
![主要方法](https://raw.githubusercontent.com/lish44/pic/main/res/202205162328807.png)

### CGI程序
对 Web 服务器程序调用其他程序的规则所做的定义就是 CGI，
而按照 CGI 规范来工作的程序就称为 CGI 程序。
