# Erlang
--------
### 配置
#### mac
##### vscode 
+ 先安装 `brew install erlang`，位置在`/usr/local/Cellar/erlang/24.1.3` 
+ 然后配置环境变量
```bash
export PATH="/usr/local/Cellar/erlang/24.1.3/bin:$PATH"
export PATH="/usr/local/Cellar/erlang/24.1.3/lib/erlang/bin:$PATH"
export MANPATH="/usr/local/opt/erlang/lib/erlang/man:$MANPATH"
```
+ 去[这个](https://erlang-ls.github.io/configuration/) 页面copy配置文件，文件放在`> filename:basedir(user_config, "erlang_ls").` 输出的目录下。配置文件的第一行opt_path 要填`/usr/local/Cellar/erlang/24.1.3/lib/erlang`  
+ 下载erlang_ls拓展就没问题了

### 基本

附注是以连字符开头的事物（例如-module和-export）

`-module(main).` 
+ 模块名 也要和文件名一样，相当于类

变量必须要大小首字母，不同函数里面的同名变量没有联系，一开始就会被绑定

`f()` 清空

`b()` 查看绑定的变量

`h()` 看历史记录

#### 变量
[https://iowiki.com/erlang/erlang_variables.html](https://iowiki.com/erlang/erlang_variables.html) 


#### 编译文件
`c(ModuleName).` 
+ 编译完了会产生一个 当前文件名字.beam的目标代码文件


#### float
整数除整数 必定得到 float，除非用 `div` `rem`
+ 5 div 3 % -> 1 会舍去余数
+ 5 rem 3 % -> 2 直接取余
+ Erlang在内部使用64位的IEEE 754-1985浮点数

#### 原子(Atom)
> 类似于枚举，c里面的宏定义，原子应以小写字母开头，可以包含小写和大写字符，数字，下划线(_)和“at”符号(@) 。 也可以用单引号括起原子 cat = 'cat' 是一个意思 

#### 元组(tuple)
> 用{}括起来，用逗号分割

比如创建一个坐标

`P = {10, 20}` 

提取里面的值

```
{X, Y} = P.
X. % 10
```

创建一个人
```erlang
Person = {person, {name, jack}, {height, 183}, {footsize, 43}}.
```


提取里面的值
```
{_,{_,Name},{_,_},{_,_}} = Person.
Name. % jack
```

#### 列表
> 用[] 括起来，用逗号分割。 里面可以装任何事物，里面分了表头和表尾 用 “|” 分割

```erlang
QWE = [{qwe,1},{asd,2}].
[Opt1 | Opt2] = QWE.
```
+ Opt1 就是表头
+ Opt2 就是表尾

要追加表
```erlang
QWE1 = [{qaz,3},{wsx,4} | QWE].
[Opt3 | Opt4] = QWE1.
```
+ Opt3 就是表头 {qaz, 3}
+ Opt4 就是表尾 [{wsx,4},{qwe,1},{asd,2}]

### 逗号 句号 分号
+ 逗号（,）分隔函数调用、数据构造和模式中的参数
+ 分号（;）分隔子句。我们能在很多地方看到子句，例如函数定义，以及case、if、try..catch和receive表达式。
    - 同函数同参数要用；而且参数一样的要放在一起
+ 句号（.）（后接空白）分隔函数整体，以及shell里的表达式。
+ 句号分隔句子，分号分隔子句，逗号则分隔下级子句。逗号象征短程，分号象征中程，句号则象征长程。

### 匿名函数
```shell
> Double = fun(X) -> 2*X end.
```

