# 基础概念

--------

Docker 就是一个虚拟机

### image container tar dockfile 关系

image 类似于虚拟机中的system iso文件，其实就是一个模板 run 之后 就变成一个 container 了

tar 可将image 直接保存成tar 类似于vm中的vmdk文件，然后可以把tar给其他人，他人拿到直接 load 就可 -> image直接使用

dockfile 配置文件 就是说明如何构建一个image

底层原理

docker 是个 CS 结构，docker的守护进程在运行的宿主机上，通过socket从客户端访问

docker-server是一个后台服务

docker-client是一个前台指令

[一个在线试用4h的docker的免费网站](https://labs.play-with-docker.com/) 

[【docker入门】10分钟，快速学会docker-哔哩哔哩】](https://b23.tv/vKEUilx)

### 基本命令

```docker
# 首先从本地看是否有image，没有就从docker-hub pull image，然后下载到本地后执行dockerfile 
docker run <image> 

# -d 后台运行  -p 将容器的 80 端口映射到主机的 80 端口
docker run -d -p 80:80 docker/getting-started

# 获取一个image
docker pull <image>

# 查看image
docker image ls 

```

[基础教程](https://www.kuangstudy.com/bbs/1591000004590710785) 

[配套手册](https://yeasy.gitbook.io/docker_practice/image/pull) 

![pic](https://raw.githubusercontent.com/lish44/pic/main/res/202206111313865.png)
