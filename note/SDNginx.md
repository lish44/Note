### Nginx 反代
--------

如果想用 Nginx 反代 WebUI，需要注意：WebUI 里面用到 websocket，所以反代也需要考虑到，不然 WebUI 中发出的 ws 请求 /queue/join 会一直报错，下面放一下我的反代的配置：

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name xxx.xxx.com;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl;
    listen [::]:443 ssl;
    server_name xxx.xxx.com;

    ssl_certificate /etc/nginx/cert/xxx.pem;
    ssl_certificate_key /etc/nginx/cert/xxx.key;

    proxy_connect_timeout              60s;
    proxy_send_timeout                 60s;
    proxy_read_timeout                 60s;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Upgrade           $http_upgrade;
    proxy_set_header Connection        $connection_upgrade;
    proxy_set_header X-Forwarded-Proto $scheme;

    location / {
        proxy_pass http://localhost:7860;
    }
}
```
使用上述配置还需要在 nginx.conf 中的 http 模块中添加上如下声明，不然会报错：
```nginx
map $http_upgrade $connection_upgrade {
    default upgrade;
    ''      close;
}
```

