### Win 装 Nvim
--------

### 安装nvim

下载nvim window64.zip版本

[https://github.com/neovim/neovim/releases](https://github.com/neovim/neovim/releases)

解压后放在喜欢位置 如 D:\Editor

### 添加环境变量

把文件所在位置的bin目录路径添加到系统环境变量

cmd 输入 sysdm.cpl 打开环境变量 高级->环境变量

![pic](https://gitee.com/rehma/pic/raw/master/res/20210912161149.png)

![pic](https://gitee.com/rehma/pic/raw/master/res/20210912161207.png)

![pic](https://gitee.com/rehma/pic/raw/master/res/20210912161220.png)


基本安装完成

### 配置文件

init.vim 位置

```plain
~/AppData/Local/nvim/init.vim  
```
* `/` Linux只能使用正斜杠
* win `/` `\` 都能用 只不过在编程中 `\` 会被当做转义符号 所以`D:\\Test`
* Local 下没有nvim文件夹自己创建 init.vim 也自己创建
* [https://github.com/lish44/ConfigurationFile/blob/main/.vimrc](https://github.com/lish44/ConfigurationFile/blob/main/.vimrc)
### Vim-Plug 安装

GitHub地址：[https://github.com/junegunn/vim-plug](https://github.com/junegunn/vim-plug)

克隆到本地用 PowerShell

```plain
iwr -useb https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim |`
    ni "$env:LOCALAPPDATA/nvim-data/site/autoload/plug.vim" -Force
```
* 位置就在 ~/AppData/Local/nvim-data/site/autoload
* 主要就是 plug.vim 这个文件 把它复制到 ~/AppData/Local/nvim/autoload 这个文件里面autoload没有自建

init.vim 添加下面两句

```plain
call plug#begin('Path')
"Plug'vim-airline/vim-airline'
"TODO::
call plug#end()
```
* path 就是插件安装存储的位置 随意

vim里面执行 PlugInstall 安装

如果提示git 不存在 需要安装Git 

