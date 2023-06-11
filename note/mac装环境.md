最开始没有git, 可以先装Xcode 开发工具命令行工具, 不用把整个xcode环境装下来

```
xcode-select --install 
```

然后下个 [clashx](https://github.com/yichengchen/clashX/releases) 开全局安 [brew](https://brew.sh/) 和 [oh my zsh](https://ohmyz.sh/#install) , zsh 要配置host不然找不到, ip [这里](https://ip.tool.chinaz.com/raw.githubusercontent.com)查

zsh 装插件在 [这里](https://github.com/lish44/Note/blob/main/note/zsh.md) 

```bash
vim /etc/hosts

# 这句话加进去
185.199.108.133 raw.githubusercontent.com
```

然后就可以关了clash配置自己的proxy了, 把所有代理走socks5

```zsh
alias proxyon='export ALL_PROXY=socks5://127.0.0.1:10808'
alias proxyoff='unset ALL_PROXY'
```

安装软件和包

```
brew install --cask google-chrome font-source-code-pro font-profont-nerd-font temurin8 IINA tabby 1password vscode

brew install wget Raycast Wechat qq alacritty fzf lazygit rust neofetch font-hack-nerd-font miniconda picgo tumx node snipaste 1password tmux nvim temurin go goland mysql htop bat

```

配置都在[这里](https://github.com/lish44/config-back) , 放到对应位置即可





