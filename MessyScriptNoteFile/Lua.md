# Lua 基本语法
--------

### 类型
__nil__

__boolean__ 

__number__ 

__string__ 

__function__ 

__userdata__ : 表示任意存储在变量中的C数据结构

__thread__ : 表示执行的独立线路，用于执行协同程序

__table__ : Lua 中的表（table）其实是一个"关联数组"（associative arrays），数组的索引可以是数字、字符串或表类型。在 Lua 里，table 的创建是通过"构造表达式"来完成，最简单构造表达式是{}，用来创建一个空表。

### 变量生命周期
```lua
a = 5               -- 全局变量
local b = 5         -- 局部变量

function joke()
    c = 5           -- 全局变量
    local d = 6     -- 局部变量
end

joke()
print(c,d)          --> 5 nil

do
    local a = 6     -- 局部变量
    b = 6           -- 对局部变量重新赋值
    print(a,b);     --> 6 6
end

print(a,b)      --> 5 6
```
### 表
#### 一维数组
```lua
tb = {1, 2, nil, 3,"huahua"} -- 类似List<object>
print(#tb) -- 5 前面版本#判断长度遇到nil会断 后面好像修复了
```
#### 二维数组
```lua
tb = {{1, 2, 3}, {4, 5, 6}}
print(tb[1][3]) -- 3
```
+ tb第一个[1] 代表第一个数组{1,2,3}，后面的[3] 代表里面的第三个元素

#### 迭代
__ipairs__ : 遇到不连续的key会断开

__pairs__ : 不会

#### json和table的关系
```json
{
    "scripName": "脚本测试",
    "breathTime": 1000,
    "initScreen": 0,
    "main": [
        {
            "type": "DEBUG",
            "title": "debug 测试1"
        }
    ]
}
```

```lua
resJson = {
    main = {{
        ["type"] = "DEBUG"
    }}
}
```

__调用__ : `resJson.main[1].type` resJson在lua里面就是个table，在json里面就是最外的括号






