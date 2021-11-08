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

```lua
type() //查类型

nil 空类型
number -> int float double
boolean -> bool
没有char

//直接声明
age = 10
name = 'rehma' //单双引号都行

```
更多数据类型 [https://www.runoob.com/lua/lua-data-types.html](https://www.runoob.com/lua/lua-data-types.html)

### 注释
```lua
-- 单行注释
--[[
    多行注释
--]]
```
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
### 表(Table)

table 是lua中一种数据代码结构 可以看做是一个对象 可以进行操作

table 和 数组的关系 - - 其实就是 面粉和馒头关系 面粉不但可以做馒头 还可做面条

语法
```plain
table_name = {item1, item2 ...}

item 可以是 1，2，3等数值类型 这就是数组
也可是 1，'rehma' 等混合 这就是集合
也可是 1 = '小明', 2 = '小红'等 k v 结构 
可以是 'jack' = 10, 'hhh' = 'apple' 等键值对
```
+ 调用的话直接用 . -- 想象成 tb.k 得到 v（有可能是值或者方法或者一个表达式，但无所谓，最终用表.k就能拿到k对应的v）

+ 如果是数组 用 ipairs 如果是键值对 用pairs
#### 一维数组
```lua
tb = {1, 2, nil, 3,"huahua"} -- 类似List<object>
print(#tb) -- 5 前面版本#判断长度遇到nil会断 后面好像修复了

arr = {1,2,3} --数组下标从1开始
arr = {name = "jack", age = 10, ["profession"] = "student"} --字典k v
```

```lua
arr = {1, 2, 3}
arr1 = {1, 'asd', true, 1.1}
```
取数组长度时可以用 **#** 这里数组必须是不包含 **nil** 但是最好不要在lua使用
数组下标从 1 开始

```lua
arr1 = {1, 'asd', true, 1.1}
for i = 1, #arr 1 do
	print(arr1[i]) -- 1 'asd' true 1.1
end
```

#### 二维数组
```lua
tb = {{1, 2, 3}, {4, 5, 6}}
print(tb[1][3]) -- 3
```
+ tb第一个[1] 代表第一个数组{1,2,3}，后面的[3] 代表里面的第三个元素
 
```lua
arr = {} -- 空表
for i = 1, 3, 1 do
	arr[i] = {} -- 表的元素又是表 婊中婊 这样就建立了二维
	for j = 1, 3, 1 do
		arr[i][j] = i * j
	end
end
-- 遍历
for i = 1, #arr do
	for j = 1, #arr[i] do
		print(arr[i][j])
	end
end
```

#### 迭代
__ipairs__ : 遇到不连续的key会断开

__pairs__ : 不会

#### 遍历
```lua
--1 for 从下标1 开始取 后面1代表自增++
arr = {1,2,3}
for i = 1, #arr, 1 do --#取arr的len，数组连续时有用
	print(arr[i])
end
-- 
```

### json和table的关系
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


### 特殊符号和运算符

**+** 这个符号只能是数学上用 连接用 **..**

```lua
a = 10 b = 20
c = a + b
print('结果:' .. c) //结果:30
```
没有 __++ --  += -=__ 操作符
```plain
a = 10
a = a + 1 // ++操作 += 1操作
```
算术运算符 **+ - * / %** 加减乘除和c#一样
```lua
a = 10
a = a + 1
a = a - 1
a = a * 2
a = a / 2
a = a % 2
```
关系运算符 **> < >= <= == ~=**
```lua
a = 10 b = 20
if(a ~= b) -- 只有不等于不一样
then
   print('a 不等于 b')
end
```
**=** 多值交换
```lua
a = 10 b = 20
a, b = b, a
print('a等于:' .. a .. 'b等于:' .. b) 
```
**&& || !** 对应 **and or not**
### 流程语句

if

```lua
if (条件) then 
    --TODO:: 
end
```
if else
```lua
if (0) then -- 0 在lua中代表true 
  --TODO::
else
  --TODO::
end
```
if else if else
```lua
if (条件) then
    --TODO::
else if (条件) then
    --TODO::
else
    --TODO::
end
```

**Lua 没有 switch语句**

### Loop语句

#### for

exp1 到 exp2 的过程 exp3是过程执行的条件

```plain
for var=exp1,exp2,exp3 do  
    <执行体>  
end  
```
for  i从赋值的数开始 每次默认步长 +1 
```lua
for i = 1, 3 do
	print(i) -- 1 2 3
end

-- 步长 +2
for i = 1, 6, 2 do
	print(i) -- 1 3 5 
end

-- 步长 -1
for i = 5, 1, -1 do
	print(i) -- 5 4 3 2 1 
end
```
exp3 可以是函数
```lua
function f(x)  
    print("function")  
    return x*2  
end
-- f执行一次 返回 4 所以 exp2 值为4 
for i = 1, f(2) do 
    print(i)-- function 1 2 3 4
end
```

#### while ... do

```lua
while (条件) do
    --TODO::
end
```
#### do ...while

```lua
repeat
    --TODO::
until (条件) -- 条件为假才执行！！！
```
lua 中没有continue 用 do while 模拟
```lua
for i = 1, 3 do
    repeat
        if i == 2 then
            break
        end
        print(i) -- 1 3
    until true
end
```

### 数组

一维数组


二维数组

### 函数

```plain
function function_name( ... ) --参数直接写可以不用写类型
	-- body
    -- return 如果有就有返回值
end
```
函数可直接做参数传递
```lua
function Add( a, b )
	return a + b
end

function Fun( a, b, fun )
	return fun( a, b)
end

print(Fun(10,20,Add))
```

### 作用域

~~变量的作用域由声明这个变量的位置决定 { } 内有效~~

~~声明在方法内部称为局部变量 -> 只能在方法体内部使用~~

~~声明在类中的成员变量称为全局变量 -> 当前类中任意位置都可以访问~~

只要不加 **local** 都是全局作用域

```lua
age = 10

function Fun ()
    name = "hhh"
    local class = '二班'
end

print(name) -- nil 未初始化
Fun()
print(name) -- hhh
print(class) -- 局部的 没权访问
```

### 字符串

三种 **''** 单引号 **""** 双引号 **[[]]** 全字符输出

```lua
str1 = 'qwe'
str2 = "asd"
str3 = [[zxc 
1
]]
--str3 保留了中间所有字符
print(str1, str2 ,str3) -- qwe	asd	zxc 
1

```
基本常用api
```lua
str = 'qwe'
str = string.upper(str)
print(str)
str = string.lower(str)
print(str)
str = string.reverse(str)
print(str)
str = string.gsub(str,'ewq','reverse') -- string.gsub（待替换串，旧串，新串，次数默认全替换）
print(str)

```

### table

#### 元表 metatable
两个tbale相互关联产生“附属”关系，只需操作主表，就能间接操作元表
```lua
tableA = {name = "monkey", age = 10}
tableB = {names = "jack" ,ages = 20}

setmetatable(tableA,tableB) --关联两个表，前者主表，后者元表
tableA = setmetatable({}, {}) -- 可以直接写成一行

getmetatable(tableA) -- 判断table是否有元表，没有返回nil，有返回地址

-- __index索引
print(tableA.name) -- 通过.访问 和table["name"] 一样
print(tableA.names) -- 报错！没有设置元表index

tableB.__index = tableB -- 通过索引index让元表指向自身
tableA = setmetatable({}, {__index = tableB}) --简写
print(tableA.names) -- 可以访问 
```

#### 面向对象
```lua
--模拟创建类 name是字段
Animal = {name}
-- 模拟构造函数 
function Animal:New( name )
	local obj = {}
	setmetatable(obj,self)
	self.__index = self
	self.name = name
	return obj
end
-- 类的成员函数
function Animal:Print()
	print(self.name)
end
-- 对象实例化
dog = Animal:New("wangcai")
dog:Print()-- 放调用用：属性调用用.


--继承!
cat = Animal:New() -- 模拟继承
function cat:New( name )
	local obj = Animal:New(name) 
	setmetatable(obj,self)
	self.__index = self
	self.name = name -- 字段赋值
	return obj
end

c = cat:New("cat")
print(c.name) -- 调用字段用.
```

#### 代码分离
Animal类
```lua
Animal = { name }
function Animal:New( name )
	local obj = {}
	setmetatable(obj,self)
	self.__index = self
	self.name = name
	return obj
end

function Animal:DebugLogName()
	print(self.name)
end
```
Persion类
```lua
Persion = {name, age, gender}

function Persion:New( name, age, gender )
	local obj = {}
	setmetatable(obj,self)
	self.__index = self
	self.name = name
	self.age = age
	self.gender = gender
	return obj
end

function Persion:DebugLog ()
	print(string.format("名字:%s,年龄:%s,性别%s",self.name, self.age, self.gender))
end
```
**mian类** 
```lua
dofile ("Animal.lua") -- dofile关键字引入 括号填路径 
dofile ("Persion.lua") 
--[[
    相对路径：
        上级 ..\\两斜杠代表一斜杠有转义的意思
        ex: ("class//Animal")
            ("..//class//Animal") main本身不在根目录，需要返回上一级再寻找
    绝对路径：
        实际用的少
--]]


cat = Animal:New("tom")
rehma = Persion:New("rehma", 10, "man")

cat:DebugLogName()
rehma:DebugLog()
```






