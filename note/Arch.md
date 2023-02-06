# Arch
--------

### 下载
[http://mirrors.163.com/archlinux/iso/](http://mirrors.163.com/archlinux/iso/) 

### 安装

### 开始禁用
`systemctI stop reflector. service` 

### 设置系统时间
`timedatectl set-ntp true` 

### 分区
`parted /dev/sda` 进行磁盘变更

+ `mktable` 
+ `gpt` 
+ `quit` 

`cfdisk` 命令进行分区
+ `cfdisk /dev/sda` 
![分区窗口](https://raw.githubusercontent.com/lish44/pic/main/res/202205162323916.png)

+ 首先分800M的EFI分区
+ 30G的根目录分区
+ 剩下的是home分区
+ 然后写入 最后退出

可以用 `fdisk -l`  查看

### 格式化分区
`mkfs.ext4 /dev/sda2`
`mkfs.ext4 /dev/sda3` 

`mkfs.vfat /dev/sda1` 

### 挂载
![挂载](https://raw.githubusercontent.com/lish44/pic/main/res/202205162324405.png)

### 设置时区
+ `In -fs /usr/share//zoneinfo/Asia/Shanghai /etc/localtime` 
+ `hwclock --systohc` 




#### 换源
`` 

### database锁定
`rm -f /var/lib/pacman/db.lck` 

