
安装
```bash
brew search temurin
brew install temurin17
```


mac下查看安装的版本
``` bash
/usr/libexec/java_home -V
```

切换到特定版本的 Java
```
export JAVA_HOME=$(/usr/libexec/java_home -v <version>)
```
+ 其中 <version> 是要切的 Java 版本号，如 1.8 或 17


### contos8
```bash

sudo yum -y install java-17-openjdk.x86_64 java-17-openjdk-devel

```
