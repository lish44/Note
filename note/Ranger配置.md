# Ranger 配置
/Users/rehma/.config/ranger/rc.conf
--------


### 安装 

`brew install ranger` 

生成配置文件

`ranger --copy-config=all`  - - 可通过 **ranger -h** 查看参数

本机配置文件目录

`/Users/<username>/.config/ranger`  

[配置文件 GitHub](https://github.com/lish44/ranger) 

### 文件操作

创建文件夹

`cfn` 

创建文件

`cn` 

重命名文件夹
```
cw	全部重新命名
cfq	在最前面加名
A	在后面加名字
a	在后缀前改
```

### Tab 操作

打开一个Tab

`<C-n>` 

切换Tab

`tab` 

关闭一个Tab

`<C-w>` 

### 装图标和字体

先装字体

[https://github.com/ryanoasis/nerd-fonts](https://github.com/ryanoasis/nerd-fonts) 

再装图标

[https://github.com/alexanderjeurissen/ranger_devicons](https://github.com/alexanderjeurissen/ranger_devicons) 

在rc.conf附加 使其生效
```
echo "default_linemode devicons" >> $HOME/.config/ranger/rc.conf
```

### 终端下看图片 

shell下的预览插件只限于iterm2

先用curl 克隆出这个shell文件 位置在家目录 ~/
```
curl “https://iterm2.com/utilities/imgcat” > imgcat 
```

然后 用chmod给添加权限
```
chmod +x ./imgcat
```

然后移动到bin目录
```
sudo mv imgcat /usr/local/bin/
```

最后再给最高权限
```
sudo chmod 777 /usr/local/bin/imgcat
```

### Pandoc 坑

安装
```
brew install pandoc
```

需要渲染器

[https://miktex.org/download](https://miktex.org/download) 

pandoc 问题

[https://www.jianshu.com/p/dcc2f95cc086?utm_campaign=maleskine](https://www.jianshu.com/p/dcc2f95cc086?utm_campaign=maleskine) 


[return](./index.md)
