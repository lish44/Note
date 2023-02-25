Expires 是 HTTP 协议中的一个头部字段，用于指定资源的过期时间。如果浏览器请求的资源已经过期，那么它会再次发送请求到服务器以确保得到最新版本。

Expires 的值是一个 GMT 时间，通常是当前时间加上一段时间间隔，比如几天、几小时或者几分钟。

例如：
```http
Expires: Thu, 15 Apr 2021 20:00:00 GMT
```
在这个例子中，资源的过期时间是 2021 年 4 月 15 日 20:00 GMT。当客户端请求该资源时，如果当前时间已经晚于 2021 年 4 月 15 日 20:00 GMT，那么它会重新发送请求以确保得到最新版本。

使用 Expires 头部字段可以提高网站的性能，因为客户端可以在不需要与服务器通信的情况下缓存资源。但是，如果资源经常发生更改，那么把 Expires 设置为很短的时间可以避免客户端使用过期的资源。