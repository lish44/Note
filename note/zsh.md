# zsh 配置
--------

### 下载安装
wget 代理后去[官网](https://ohmyz.sh/)下载 

### 配置

```bash
// 高亮和自动补全插件
git clone https://github.com/zsh-users/zsh-syntax-highlighting ~/.oh-my-zsh/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/plugins/zsh-autosuggestions
```

然后`.zshrc` 配置
```zsh
plugins=(
    zsh-autosuggestions
    zsh-syntax-highlighting
)
```

[其他参考](https://zhuanlan.zhihu.com/p/381064954) 

