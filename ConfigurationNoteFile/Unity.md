### unity
--------

首先unity 要有 .sln和Assembly-CSharp.csproj 文件 没有就用vscode 生成

然后安装[omnisharpvim](https://github.com/OmniSharp/omnisharp-vim) 。
    
1. `let g:OmniSharp_server_use_mono = 1` 
2. 安装roslyn 自动安装非常慢 改手动 [地址](https://github.com/OmniSharp/omnisharp-roslyn/releases) 位置默认在`/Users/rehma/.cache/omnisharp-vim/` 下
3. 设置 `let g:OmniSharp_server_path = '/Users/rehma/.cache/omnisharp-vim/omnisharp-roslyn-v1.38.2/.exe'` 照理说mac是 run 文件 但是 用exe也行 
