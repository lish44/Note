# nvim折腾
--------

### nvim 的配置文件
vim 配置文件的原始路径在

```plain
/Users/<user>/.vimrc
```
nvim 配置文件在
```plain
/Users/<user>/.config/nvim/init.vim
```

有.vimrc文件的话 可以直接用 **cat >** 连接写入进去

~/ 代表 home目录 （Users/<user>）

```plain
ex: ~/.vimrc > ~/.config/nvim/init.vim
```
还可用 **ln -s** 直接链接过去   
```plain
作用：
  当我们需要在不同的目录，用到相同的文件时用 不必重复的占用磁盘空间
ln -s [源文件] [目标文件] 
```

```plain
ln -s ~/.vimrc ~/.config/nvim/init.vim
```
以后改.vimrc 相应的init.vim也会随之更改
### vim高级使用

#### 连贯递增

```plain
"ayw
```
先用a寄存器存一个数字 
```plain
qq"ap^a"aywjq 
```
* qq 宏录制
* "ap 把寄存器a的值复制出来
* ^a 就是 <c-a> 让数字++
* "ayw 把当前已经++了的值重写存到寄存器a里面
* jq 往下走一行 结束录制
### 插件

#### markdown

[https://github.com/iamcco/markdown-preview.nvim](https://github.com/iamcco/markdown-preview.nvim)

```plain
Plug 'iamcco/markdown-preview.nvim', { 'do': { -> mkdp#util#install() }, 'for': ['markdown', 'vim-plug']}

Plug 'iamcco/markdown-preview.nvim', { 'do': 'cd app && yarn install'  }

```
* 必须装 nodejs 和 yarn
* 插件目录的app文件夹下 **yarn install**
### mac 装输入法切换

[https://github.com/daipeihust/im-select/releases](https://github.com/daipeihust/im-select/releases)

* 下载文件并放到 **/usr/local/bin/**下
* 然后vs里面json设置
```plain
"vim.autoSwitchInputMethod.enable": true,
"vim.autoSwitchInputMethod.defaultIM": "com.apple.keylayout.ABC",
"vim.autoSwitchInputMethod.obtainIMCmd": "/usr/local/bin/im-select",
"vim.autoSwitchInputMethod.switchIMCmd": "/usr/local/bin/im-select {im}"
```
* 退出默认切换成apple输入法 ，然后还要再搜狗设置默认是英文进入
### vim插件

#### dyng/ctrlsf.vim 全局搜索插件

[https://github.com/dyng/ctrlsf.vim](https://github.com/dyng/ctrlsf.vim)

* leader f 开起搜索
* o 覆盖原有文件打开
* t 新标签打开
* p 在右边分屏打开
* P 同p在左边
* q 退出
* Ctrl j/k 上下匹配移动

