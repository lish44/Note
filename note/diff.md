# Vim 对比

--------

> 一二方法适用于新内容对比（就是没有存在文件里的）

> 三四方法适用于文件对比

> `<file>` 是文件名 `<folder>` 是文件夹名

### 方法一

新一个文件夹 然后新建两个文件 用  对比

快速新建文件: `mkdir <folder> ; cd <folder> && echo "内容1" > <file_1> && echo "内容2" > <file_2>` 

对比: `vim -d <file_1> <file_2>`

**ex:**

`mkdir huahua && cd huahua && echo "qwe" > qwe && echo "qwe asd" > asd` 

`nvim -d qwe asd` 

操作比较慢但是可以用拥有源文件比较的记录

~~创建文件夹再进去有点麻烦，可以在bash或zsh里映射个 `mkcd` 命令就可直接创建并进入~~

```bash
alias mkcd='function __mkcd(){ if [ $# == 1 ]; then mkdir $1; cd $1; unset -f __mkcd; elif [ $# == 2 ]; then mkdir $1 $2; cd $2; unset -f __mkcd; fi }; __mkcd'
```


### 方法二

在vim里面直接通过buffer比较

命令行里 `vim <file_1>` 新建一个buffer ，然后粘贴内容1，不用保存。然后在buffer1里 `:n <file_2>` 新建一个buffer2，
粘贴内容2，然后`:vert diffsplit <file_1>` 

操作起来快但是没有缓存

### 操作命令
`]c` : 下个差异点

`[c` : 上个差异点

`diffput` : 当前差异点复制到另一个文件

`diffget` : 差异点复制到当前文件

`diffupdate` : 修改后的更新，vimdiff也会自动来重新比较

**上下文展开和查看**

缺省会把差异处上下各6行的文本都显示出来，可通过以下修改

`:set diffopt=context:6`

`zo` : 展开折叠的行

`zc` : 重新折叠

--------

参考：

[https://linuxhint.com/diff-two-files-vim/](https://linuxhint.com/diff-two-files-vim/) 
