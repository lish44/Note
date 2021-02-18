# 安装

+ `brew install mysql` 如果安装慢切换brew源
    > 阿里源
    ```
    # 替换brew.git 
    cd "$(brew --repo)" git remote set-url origin https://mirrors.aliyun.com/homebrew/brew.git 
    # 替换homebrew-core.git 
    cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" git remote set-url origin https://mirrors.aliyun.com/homebrew/homebrew-core.git 
    # 刷新源 
    brew update
    ```

+ `brew info mysql` 如果cmake报❌，重新安装一下
    > `brew unlink cmake`
    
    > `brew install cmake`
