# 缓冲区
--------

> buffer 就是一块内存区域，所写的内容都在这块区域里头，退出了如果没保存（写入）到某个文件里面去的话，就会丢失。

### 添加buffer

```bash
:vi file1 file2
```
+ 可以创建buffer 后面参数就是创建的几个
+ `:ball`命令可以给每个 buffer 打开一个窗口

### buffer标识
| 状态 |                             含义                             |
|:----:|:------------------------------------------------------------:|
|  -   |       Readonly buffer 禁用了modifiable选项，只读缓冲区       |
|  =   |                  Readonly buffer 只读缓冲区                  |
|  a   |          Active buffer 活动缓冲区，当前显示在屏幕上          |
|  h   |      Hidden buffer 隐藏缓冲区 已载入但没有显示在屏幕上       |
|  +   |                Modified buffer 已更改的缓冲区                |
|  x   |               Error buffer 读入时报错的缓冲区                |
|  %   |                  Current buffer 当前缓冲区                   |
|  #   |                 Alternate buffer 交换缓冲区                  |
|  u   | Unlisted buffer 只有在列示命令中使用！修饰符才能显示的缓冲区 |
+ 使用“!”修饰符的 `:buffers!` `:files!` `:ls!` 命令将会列出包括“u”类型在内的所有缓冲区信息

### 操作

```
:buffer number
:buffer filename
```
+ number选择指定缓冲区
+ filename文件名选择指定缓冲区

```
:bnext
```
+ 切下一个

```
:bprevious
:bNext
```
+ 切前一个

```
:blast
:bfirst
```
+ 切最后一个和切第一个

```
:bdelete filename
:bdelete 3
:3 bdelete
:1,3 bdelete
```
+ 删

### Buffer、Window 和 Tab 之间的关系
buffer 单位最小就是一块内存区域，Window就是用来展示这个区域的，一个buffer可以再不同的Window里面显示（也就是说但都是指向的同一个buffer内存区域，一个改变另外一个也更到变）

在 Vim 中这三者的关系大概是这样的：Buffer 负责保存数据，Window 负责展示数据，Tab 为 Window 提供排版布局，Buffer 和 Tab 对 Window 总是一对多的关系。如果把 Vim 想象成一个机房的话，Buffer 就是主机，Window 是显示器，而 Tab 是一个个显示器架子。只不过这个机房里面的显示器可以随意连接到别的主机上面，一个主机可以被多个显示器连接。

### 参考

[https://zhuanlan.zhihu.com/p/27616958](https://zhuanlan.zhihu.com/p/27616958) 

[https://blog.csdn.net/jy692405180/article/details/79775125](https://blog.csdn.net/jy692405180/article/details/79775125) 
