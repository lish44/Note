### Lua基本语法

### table
```lua
arr = {1,2,3} --数组下标从1开始
arr = {name = "jack", age = 10, ["profession"] = "student"} --字典k v
```
三种遍历
```lua
--1 for 从下标1 开始取 后面1代表自增++
arr = {1,2,3}
for i = 1, #arr, 1 do --#取arr的len，数组连续时有用
	print(arr[i])
end
-- 
```

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


