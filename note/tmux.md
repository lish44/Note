# Tmux 

--------

### 一些概念

- server 服务：是整个tmux的后台服务

- session 会话：就是终端窗口打开后与shell的一次 **"绑定"**，如服务器ssh登录后就是一次session，突然断开后再登录就找不到上次执行命令，因为会话终止，其进程随之消失。session的存在可保存当前状态 (一般可以当成一个工作区)

- window 窗口：一个窗口对应一个pane，或多个窗口对应一个pane，pane就活在window里面
 
- pane 窗格：里面的分屏

![tmux概念](https://raw.githubusercontent.com/lish44/pic/main/res/202205272337040.png)

### 一些操作

<font color=#bf616a>以下 <font color=#81a1c1>按键</font> 都带前置操作（Prefix-Command）</font> <kbd>ctrl-b</kbd> 

session
--------

创建session `tmux new -s <session_name>` 

删除指定session `tmux kill-session -t <num> or <session_name>` 

改名 <kbd>$</kbd>

暂时分离session <kbd>d</kbd>

附加session `tmux a -s <session_name>` 如果只要一个session可 直接 `tmux a`  

查看所有session  <kbd>s</kbd>

window
--------

创建window <kbd>ctrl-b</kbd> <kbd>c</kbd> 

关闭window <kbd>ctrl-b</kbd> <kbd>&</kbd> 

切换window <kbd>ctrl-b</kbd> <kbd>n</kbd> | <kbd>p</kbd> 

改名 <kbd>,</kbd>

pane
--------

创建横竖分割窗格 <kbd>v</kbd> | <kbd>h</kbd> (需要设置映射)

上下左右选择窗格 <kbd>up</kbd> <kbd>down</kbd> <kbd>left</kbd> <kbd>right</kbd> 

窗格切换 <kbd>o</kbd> | <kbd>;</kbd> 

窗格交换 <kbd>{</kbd> | <kbd>}</kbd> 

关闭窗格 <kbd>x</kbd> 

放大缩小pane <kbd>z</kbd>

一些设置
--------

```tmux
unbind C-b
set -g prefix C-l
set -s escape-time 0
set -g mouse on // tmux 和 vim 的 esc 有冲突，需要设
set -g default-terminal "screen-256color"

# 启用活动警告
setw -g monitor-activity on
set -g visual-activity on

# Set easier window split keys
bind-key v split-window -h
bind-key h split-window -v

bind -n S-Left previous-window
bind -n S-Right next-window

# Easy config reload
bind-key r source-file ~/.tmux.conf \; display-message "tmux.conf reloaded"
```

--------

[参考链接1](https://www.ruanyifeng.com/blog/2019/10/tmux.html) 

[参考链接2](http://cenalulu.github.io/linux/tmux/) 
