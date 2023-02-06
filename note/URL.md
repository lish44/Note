# URL
--------

> 本质就是一串字符串一个路径。统一资源定位符。域名包含在这里面

### url格式

`http://user:password@www.glasscom.com:80/dir/file1.html`
+ user:password 不用写
+ http: 是协议，还有ftp:，mailto: 等，file: 就是我的电脑本机
+ www 万维网
+ glasscom.com 就是域名
+ com后面不写默认用80端口
+ /dir 的 __/__ 就是根目录，可以不写，不写默认就是 __/index.html__
    - 如果像这样 `www.xx.com/qwe` 那么qwe如果是文件就是文件，如果是文件夹就是文件目录
![url结构](https://raw.githubusercontent.com/lish44/pic/main/res/202205162327107.png)

