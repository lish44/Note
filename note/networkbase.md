#基本流程
--------

> 以http为例开始

在浏览器输入 __[URL](URL.md)__ 回车 -> 解析地址（浏览器缓存，系统缓存，路由器缓存，都没有就去DNS服务器去取）->
建立连接（tcp三握）-> 发送http请求 -> 返回http报文 -> 发完四挥 -> 浏览器DOM解析并渲染


-数据帧（Frame）：是一种信息单位，它的起始点和目的点都是数据链路层。
-数据包（Packet）：也是一种信息单位，它的起始和目的地是网络层。
-数据报（Datagram）：通常是指起始点和目的地都使用无连接网络服务的的网络层的信息单元。
-段（Segment）：通常是指起始点和目的地都是传输层的信息单元。
-消息（message）：是指起始点和目的地都在网络层以上（经常在应用层）的信息单元。
-元素（cell）是一种固定长度的信息，它的起始点和目的地都是数据链路层。

啥
