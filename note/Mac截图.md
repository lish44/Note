# Mac 截图
--------

### 换名字
```
defaults write com.apple.screencapture name "the Default Name";
killall SystemUIServer
```

### 换格式
```
defaults write com.apple.screencapture type [type];【jpg】 【gif】【PDF】【png】
killall SystemUIServer
```

### 换路径
```
defaults write com.apple.screencapture location [path];
killall SystemUIServer
```

### 去时间戳
```
defaults write com.apple.screencapture include-date -bool [true/false];
killall SystemUIServer
```
### 加快动画时间
```
defaults write com.apple.dock expose-animation-duration -int 0; killall Dock
```
### 还原动画默认时间
```
defaults delete com.apple.dock expose-animation-duration; killall Dock
```

### 长按禁用字符
```
defaults write com.sublimetext.2 ApplePressAndHoldEnabled -bool false
```

[return](./index.md)
