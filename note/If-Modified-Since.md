"If-Modified-Since" 是 HTTP 协议中的一个请求头字段。它允许客户端告诉服务器，客户端缓存中存储的文档的最后修改时间。如果服务器决定该文档已经被修改，则返回完整的响应；如果文档未被修改，则返回一个 304 Not Modified 响应，表示客户端可以继续使用其缓存的副本。

举个例子，当一个客户端请求一个 URL，并且希望获取该 URL 最新的内容：
```http
GET /example.html HTTP/1.1
Host: www.example.com
```

服务器响应：
```http
HTTP/1.1 200 OK
Last-Modified: Wed, 09 Feb 2023 10:00:00 GMT
Content-Type: text/html

<!DOCTYPE html>
<html>
<head>
  <title>Example Page</title>
</head>
<body>
  <p>This is an example page.</p>
</body>
</html>
```

当客户端再次请求这个 URL 时，如果客户端缓存了上一次的响应，则可以在请求中包含 If-Modified-Since 字段：
```http
GET /example.html HTTP/1.1
Host: www.example.com
If-Modified-Since: Wed, 09 Feb 2023 10:00:00 GMT
```

服务器根据该字段确定该文档是否已经被修改，并且只在文档已经被修改时才返回完整的响应，否则返回 304 Not Modified 响应：
```http
HTTP/1.1 304 Not Modified
```
