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


--------

### 请求报文

- 请求行 a 
- 请求体 b
- 消息体 c
![pic](https://raw.githubusercontent.com/lish44/pic/main/res/202302092132426.png)

GET请求报文
```http
GET /books/?sex=man&name=Professional HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.6)
Gecko/20050225 Firefox/1.0.1
Connection: Keep-Alive
```

### get post 区别

- get 用来一般用来请求，比如地址栏回车其实就是发了一个get请求，主要请求服务器返回的资源
- post 一般用<form>表单提交，相当于一个push操作
- get 不安全因为参数再[URL](URL.md) **?** 后面`/test/demo_form.asp?name1=value1&name2=value2 `，而post是把参数放到请求体body里面的，对于用户来说看不到. 
  ```http
  POST /test/demo_form.asp HTTP/1.1
  Host: w3schools.com
  name1=value1&name2=value2 
  ```
- get的URL长度有限，post没得
- get会被浏览器主动cache，post不得
- get刷新没事，post会重新提交表单
- get 请求在发送过程中会产生一个 TCP 数据包；post 在发送过程中会产生两个 TCP 数据包。对于 get 方式的请求，浏览器会把 http header 和 data 一并发送出去，服务器响应 200（返回数据）；而对于 post，浏览器先发送 header，服务器响应 100 continue，浏览器再发送 data，服务器响应 200 ok（返回数据）。

### 什么是cookie什么是session

因为http是无状态链接的，没有存储功能，所以为了能够支持有状态链接，cookie和session就是基于这个的实现。

- cookie存储在client，通过server发来的响应头在里面读取**Session ID**并写入浏览器，以后每次登录发送 **Session ID** 给服务就不需要重复验证。Cookie 用于存储与用户相关的数据，例如用户名、登录状态等。
- session 是一种用于在服务器端存储与客户端相关数据的技术 有超时时间 
  
### 简述 HTTP1.0/1.1/2.0 的区别

- HTTP 1.0是1996年引入的，提供了最基本的认证，使用短链接，仅使用 header 中的 [If Modified Since](If-Modified-Since.md) 和 [Expires](Expires.md) 作为缓存失效的标准，不支持断点续传，没有传递主机名的请求消息。

- HTTP 1.1是1999年出现的，对HTTP 1.0进行了改进，使用了摘要算法进行身份验证，默认使用长连接，新增了多种缓存控制标头，支持断点续传，使用虚拟网络。

- HTTP 2.0是2015年开发的标准，主要特点包括头部压缩，二进制协议，服务器推送，多路复用等。比HTTP 1.1更快，更高效，更安全。

[原文](https://zhuanlan.zhihu.com/p/135947893) 

在浏览器中输入URL回车后经历了什么
首先在浏览器缓存中查找DNS对应的ip地址 -》有就返回-》没有就向本地DNS服务器找-》没有就向根域名找-》没有就向顶级域名找-》没有就向权威DNS服务器找，然后返给本地DNS-》解析到浏览器发送三次握手建立连接，然后浏览器会发送HTTP-GET请求（长连接 1.1默认），如果是简单网站直接返回，不是的话需要重定向返回3xx链接，然后在响应报文中找location字段找到重定向地址，最后浏览器带上新URL重发，返回200ok

https

简易版过程：
1. 客户端提交https请求

2. 服务器响应客户,并把服务器公钥发给客户端

3. 客户端验证公钥的有效性

4. 有效后，客户端会生成一个会话密钥(一个随机数)

5. 用服务器公钥加密这个会话密钥后，发送给服务器

6. 服务器收到公钥加密的密钥后，用私钥解密，获取会话密钥

7. 客户端与服务器利用会话密钥对传输数据进行对称加密通信

- 过程 
  - client 发`ClientHello` 消息到server，包含TLS版本，可用的加密算法和压缩算法
  - server 收到回 `ServerHello` 包含TSL版本，server选择的加密算法和压缩算法，和CA机构签发的证书，公钥就在里面
  - 
