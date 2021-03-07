[#](#) Unity 函数生命周期

### Awake
+ <font color=#4285f4>Go</font> 初始状态为 <font color=#f4433c>Flase</font> Awake不会执行
+ <font color=#4285f4>Go</font> 初始状态为 <font color=#f4433c>True</font> Awake执行 和  **脚本本身的开启无关**
+ <font color=#4285f4>Go</font> 关闭后再次激活 和 脚本关闭后再次激活 都不会执行 Awake

### Start
+ <font color=#4285f4>Go</font> 初始状态 <font color=#f4433c>False</font>Start 不执行
+ <font color=#4285f4>Go</font> 初始状态 <font color=#f4433c>True</font> 脚本状态 <font color=#f4433c>False</font> Start不执行
+ <font color=#4285f4>Go</font> 

区别 Awake 和Go 绑定 每次Go激活<font color=#f4433c>触发</font>和 脚本自身激活无关

Start 和 脚本自身绑定 每次脚本激活<font color=#f4433c>触发</font> 和脚本的 **Enable** 属性优先级较高 对Go的优先级次要

|          Go Active状态           |            脚本enable状态             | Awake 执行结果 |     次数     | Start 执行结果 | 次数 |
|:--------------------------------:|:-------------------------------------:|:--------------:|:------------:|:--------------:|:----:|
| <font color=#0aa858>True</font>  |    <font color=#0aa858>True</font>    |      执行      | 有且仅有一次 |      执行      | 一次 |
| <font color=#0aa858>True</font>  |   <font color=#f4433c>False</font>    |      执行      | 有且仅有一次 |     不执行     | 一次 |
| <font color=#f4433c>False</font> |   <font color=#f4433c>False</font>    |     不执行     | 有且仅有一次 |     不执行     | 一次 |
| <font color=#f4433c>False</font> |    <font color=#0aa858>True</font>    |     不执行     | 有且仅有一次 |     不执行     | 一次 |

