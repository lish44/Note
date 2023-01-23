# 窗口管理
--------
### 安装

```bash
brew install koekeishiya/formulae/yabai --HEAD
brew install koekeishiya/formulae/skhd
```

开启服务
```
brew services start skhd
brew services start yabai
```

关闭服务
```
brew services stop skhd
brew services stop yabai
```

BigSur 以上配置自动加载脚本
```bash
sudo visudo -f /private/etc/sudoers.d/yabai

#然后输入一下内容，其中<user>为当前mac的用户名
<user> ALL (root)NOPASSWD: /usr/local/bin/yabai --load-sa

#然后在yabairc中添加以下命令即可
sudo yabai --load-sa
yabai -m signal --add event=dock_did_restart action="sudo yabai --load-sa"
```

### 快捷键

焦点切换

| 功能           | 快捷键               |
| :-:            | :-:                  |
| 焦点切换 ←     | <kbd>alt + h</kbd>   |
| 焦点切换 →     | <kbd>alt + l</kbd>   |
| 焦点切换 ↑     | <kbd>alt + i</kbd>   |
| 焦点切换 ↓     | <kbd>alt + j</kbd>   |
| 焦点recent切换 | <kbd>alt + tab</kbd> |
| 全屏不浮动     | <kbd>alt + f</kbd>   |
| 全屏不浮动     | <kbd>alt + d</kbd>   |

窗口操作

| 功能           | 快捷键                   |
| :-:            | :-:                      |
| 当前窗口去左边 | <kbd>alt + cmd + h</kbd> |
| 当前窗口去右边 | <kbd>alt + cmd + l</kbd> |
| 当前窗口去上边 | <kbd>alt + cmd + i</kbd> |
| 当前窗口去下边 | <kbd>alt + cmd + j</kbd> |
| 左右mirror     | <kbd>alt + cmd + m</kbd> |
| split          | <kbd>alt + cmd + e</kbd> |
| 浮动           | <kbd>alt + cmd + c</kbd> |


窗口大小

| 功能       | 快捷键                     |
| :-:        | :-:                        |
| 往左拉伸   | <kbd>alt + cmd + a</kbd>   |
| 往右拉伸   | <kbd>alt + cmd + d</kbd>   |
| 往上拉伸   | <kbd>alt + cmd + w</kbd>   |
| 往下拉伸   | <kbd>alt + cmd + s</kbd>   |
| 恢复原比例 | <kbd>alt + cmd + 0</kbd>   |

窗口发送至特定桌面

| 功能               | 快捷键                  |
| :-:                | :-:                     |
| 当前app发送至桌面1 | <kbd>alt + 1</kbd>      |
| 当前app发送至桌面2 | <kbd>alt + 2</kbd>      |
| 当前app发送至桌面3 | <kbd>alt + 3</kbd>      |
| ...                | ...                     |
| 当前app发送至桌面9 | <kbd>alt + 9</kbd>     |


桌面操作

| 功能               | 快捷键             |
| :-:                | :-:                |
| 切换桌面1          | <kbd>cmd + 1</kbd> |
| 切换桌面2          | <kbd>cmd + 2</kbd> |
| 切换桌面3          | <kbd>cmd + 3</kbd> |
| ...                | ...                |
| 切换桌面9          | <kbd>alt + 9</kbd> |
| 两个桌面recent     | <kbd>alt + 0</kbd> |

[return](./index.md)
