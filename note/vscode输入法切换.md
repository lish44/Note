# vscode输入法切换

[https://www.zhihu.com/question/303850876](https://www.zhihu.com/question/303850876)

json 添加 ctrl+shift+p 输入 >Preferences: Open Settings (Json)

```plain
"vim.autoSwitchInputMethod.enable": true,
"vim.autoSwitchInputMethod.defaultIM": "1033",
"vim.autoSwitchInputMethod.obtainIMCmd": "D:\\imselect\\imselect.exe",
"vim.autoSwitchInputMethod.switchIMCmd": "D:\\im-select\\im-select.exe {im}",
```

imselect.exe 这个程序 放到 `D:\im-select\`下

切换输入法 用 `./im-select.exe` 做测试 ex:

    英文 1033 中文搜狗 2052
