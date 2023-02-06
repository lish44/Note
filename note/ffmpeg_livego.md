# livego
--------

安装go环境
```bash
sudo apt -y install golang-go
```

更改go环境变量 不然卡
```bash
export GO111MODULE=on
export GOPROXY=https://goproxy.cn
```

下载项目
```bash
git clone https://github.com/gwuhaolin/livego.git

cd ./livego

go build
```

开端口
`1935,7001,7002,8090` 

启动服务
```bash
./livego &

nohup ./livego > log.out 2>&1 &
```

推流码 
```
http://43.136.180.100:8090/control/get?room=房间名
```

拉流地址
```
rtmp://43.136.180.100:1935/live/房间名
FLV:http://43.136.180.100:7001/live/房间名.flv
HLS:http://43.136.180.100:7002/live/房间名.m3u8
```
--------

