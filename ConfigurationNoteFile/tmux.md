# Tmux 

--------

### 一些概念

- server 服务
- session 会话
	+ 就是终端窗口打开后与shell的一次 **"绑定"**，如服务器ssh登录后就是一次session，突然断开后再登录就找不到上次执行命令，因为会话终止，其进程随之消失
- window 窗口
- pane 窗格

### 一些操作

<font color=#bf616a>以下都带激活键</font> <kbd>ctrl-b</kbd> 

创建一个window <kbd>ctrl-b</kbd> <kbd>c</kbd> 

关闭window <kbd>ctrl-b</kbd> <kbd>&</kbd> 

上下窗口切换 <kbd>ctrl-b</kbd> <kbd>n</kbd> | <kbd>p</kbd> 

创建横竖分割窗格需要设置映射 <kbd>v</kbd> | <kbd>h</kbd> 

窗格切换 <kbd>o</kbd> | <kbd>;</kbd> 

窗格交换 <kbd>{</kbd> | <kbd>}</kbd> 

上下左右选择窗格 <kbd>up</kbd> <kbd>down</kbd> <kbd>left</kbd> <kbd>right</kbd> 

关闭窗格 <kbd>x</kbd> 

删除指定session `tmux kill-session -t <num> or <session_name>` 

### 一些设置


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
