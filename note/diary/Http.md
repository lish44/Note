
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

