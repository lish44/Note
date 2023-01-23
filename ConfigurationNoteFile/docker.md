# Docker
--------

底层原理

docker 是个 CS 结构，docker的守护进程在运行的宿主机上，通过socket从客户端访问

docker-server是一个后台服务

docker-client是一个前台指令

### 一些命令

```docker
docker run  <image># 首先从本地看是否有image，没有就从docker-hub pull image，然后下载到本地后执行dockerfile 

```

[基础教程](https://www.kuangstudy.com/bbs/1591000004590710785) 
