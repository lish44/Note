# vscode 配置 c++

+ 安装gcc
+ 创建工作区文件夹
+ 添加cpp文件，里面写个主函数
+ ⇧⌘B（other）编译生成tasks.json
    ```json
    "label": "build", //任务的用户界面标签
    
    "type": "shell", //定义任务是被作为进程运行还是在 shell 中作为命令运行
    
    "command": "g++ -g hello.cpp -o hello -std=c++11", //告诉vscode要运行什么外部命令
    
    "group": {
    
        "kind": "build",
        
        "isDefault": true
        
    }, //让vs知道这是构建任务 不是命令
    
    "problemMatcher":"$gcc", //问题窗口支持错误分析
    ```

+ 在terminal运行脚本 进到目录用 ./xx 运行（不是cpp文件)
+ 点虫子 -齿轮-C++(GDB/LLDB）生成launch.json
    ```json
    "name": "(lldb) Launch", //名字
    "type": "cppdbg",
    "request": "launch",
    "preLaunchTask": "build", //这个和 tasks.json的label名一致,只运行我构建的任务 任务的用户界面标签 F5生效
    "program": "${workspaceFolder}/hello", //工作区的主文件
    "args": [],
    "stopAtEntry": false,
    "cwd": "${workspaceFolder}",
    "environment": [],
    "externalConsole": true,
    "MIMode": "lldb"
    ```

    
