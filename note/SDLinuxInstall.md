### ubuntu 安装


显卡驱动安装
```cash
#验证是否安装驱动
nvidia-smi

# 如没有进行安装
ubuntu-drivers devices
sudo apt install nvidia-driver-525
sudo rebot
```
安装对应的CUDA框架
[地址](https://developer.nvidia.com/cuda-12-0-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_local) 

配置环境变量
```bash
export PATH="/usr/local/cuda-12.1/bin/:$PATH"
export LD_LIBRARY_PATH="/usr/lcoal/cuda-12.1/lib64:$LD_LIBRARY_PATH"
```
[参考](https://qii404.me/2021/07/03/ubuntu-install-nvidia-driver.html) 

### pip下载问题



[安装参考1](https://ivonblog.com/en-us/posts/linux-stable-diffusion-webui/) 
[安装参考2](https://juejin.cn/post/7208946311886372924) 

