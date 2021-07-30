# appium
--------

### 下载appium mac版本
```
https://github.com/appium/appium-desktop/releases/tag/v1.21.0
```

### 安装依赖库 libimobiledevice 和 ios-deploy
```
brew install libimobiledevice --HEAD
npm install -g ios-deploy  #如果是iOS10以上的系统才需要安装
```
+ 如果没有安装 libimobiledevice，会导致Appium无法连接到iOS的设备，所以必须要安装，如果要在iOS10+的系统上使用appium，则需要安装ios-deploy
+ libimobiledevice 是一个跨平台的软件库 ； 不依赖任何已有的私有库，不需要越狱。应用软件可以通过这个开发包轻松访问设备的文件系统、获取设备信息，备份和恢复设备，管理 SpringBoard 图标，管理已安装应用，获取通讯录、日程、备注和书签等信息

### appium-doctor 安装
```
npm install appium-doctor -g
```
+ 安装后执行 `<++>appium-doctor --ios` 指令，可以查看与iOS相关配置是否完整

### 安装 Carthage
```
brew install carthage
```
+ Carthage项目依赖管理， 类似于 java 的 maven； 主要是 WebDriverAgent 使用，WebDriverAgent 是用它做项目依赖的

### 安装 python-client
```
git clone git@github.com:appium/python-client.git

cd python-client # 进入python-client目录
python setup.py install # 安装python-client 报错

sudo python3 setup.py install 成功
```

[传送门1](https://www.jianshu.com/p/ae8846736dba/) 
[传送门2](https://www.cnblogs.com/crstyl/p/14690895.html#ios-%E8%87%AA%E5%8A%A8%E5%8C%96%E7%9B%B8%E5%85%B3%E6%A1%86%E6%9E%B6%E4%BB%8B%E7%BB%8D) 

### 安装 ideviceinstaller
```
brew install ideviceinstaller
```

### Java jdk1.8 环境变量
jdk在`/Library/Java/JavaVirtualMachines/jdk1.8.0_211.jdk/Contents/Home` 
添加到 __.zshrc__ 

### 检测健康 appium-doctor
#### JAVA_HOME 报错需要添加环境变量到 .bash_prefile 前提要装JAVA SKD
+ `echo export "JAVA_HOME=\$(/usr/libexec/java_home)" >> ~/.bash_profile` 
+ 然后 `resouce .bash_prefile` 一下

#### ANDROID_HOME 报错
+ 先 `brew install android-skd` ，安装的位置在 `/usr/local/Caskroom/android-sdk`
+ 然后在命令行输入 `export ANDROID_HOME=/usr/local/Caskroom/android-sdk` 
+ 然后进  __.bash_prefile__  里面添加 `export PATH="$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools"` 
+ 最后 `source ~/.bash_profile` 一下搞定. 可以用`echo $ANDROID_HOME` 查看一下
[传送门](https://stackoverflow.com/questions/19986214/setting-android-home-enviromental-variable-on-mac-os-x) 
#### adb, android 报错

### ios-webkit-debug-proxy 安装
`brew install ios-webkit-debug-proxy` 
+ 这个工具在真机上访问web view。即混合应用的测试

### 安装authroize-ios
`` <++>


