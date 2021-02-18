# JavaScript基础 


### 特殊

+ 数组可以对象赋值
```javascript
var arr1 = [1,2];
var arr2 = [3,4];
arr1 = arr2;//栈拷贝，结果arr1和arr2地址相同 指向同一块区域[3,4]
```

+ 数组可以存不同类型
```javascript
var arr = [123, "asd", ture];
```

+ 值类型改变值实际在压栈(不可改变的原始值）
```javascript
int m_a = 10;//address: OxAAAA AAAA 现在m_a代表这个地址的值
m_a = 20;//address:OxAAAA AAAE 现在m_a代表这个地址得值 原来的值变成野房间，等待被覆盖
```

+ 当前**块**错误“不会”影响后面块执行，只会在控制台爆红错

+ typeof 返回6种类型
    + number
	+ string
	+ boolean
	+ undefined
	+ function
	+ object

+ 类型转换(隐示）
```javascript
console.log(3 * '8'); //24 number 加减乘除都一样
console.log('3' * '8'); //24 number

console.log(3 * null);// null会转换成0
console.log(3 * false);//false转为0
console.log(3 * true);//true转为1

console.log(3 * '9px');//NaN 不是数字，不纯的数字没办法隐式类型转换
console.log(3 * undefind);//NaN ubdefind没办法隐式类型转换
```

+ 类型转换（显示）
[传送门](https://www.cnblogs.com/weiwei-python/p/10072993.html) 

+ isNaN( )  --- 可以判断一个数是否是NaN（随机数）  
`console.log(isNaN("asd"));// true`   
`内部会做一个转换，把Number('asd')返回的结果和NaN做对比` 

+ ===和!== **(不会发生类型转换)**  
`console.log("1" === 1)// false`   
`console.log("1" == 1)// ture` 
--------

### 函数

函数声明
```javascript
function foo() {}
```

命名函数表达式
```javascript
var foo =function asd() {}
```

匿名函数表达式 --简称 函数表达式
```javascript
var foo = function () {}
```

命名表达式和匿名表达式**唯一**的区别就是输出的名字.name不一样  
弱语言类型不会输出指针，只会输出指向的空间类容

--------

### 函数参数

+ 不需要写形参类型
```javascript
function foo(a,b) {
    //var a;类型 undefind 
    //var b;调用时才确定类型
}
```

+ 内部维护了一个实参列表，所以 形参 实参 **个数** 不用一一对应(不定参数）
```javascript
function foo(a,b) {
    //arguments -- [10,20,40]
    //var a = 10;
    //var b = 20;
    console.log(arguments[2]);// 40 arguments.length 等于3
    console.log(arguments.length);//3
    console.log(foo.length);//2
}
foo(10,20,40);
```

+ 实参列表和参数一一映射
```javascript
function foo (a,b) {
   a = 99;
   console.log(arguments[0]);// 99
   console.log(arguments[1]);//undefined
}
foo (10);
```

> arguments[0] 和 a 不是同一个变量，但是内部有映射
+ 实参列表出生时有几个就有几个,只有实参形参一一对应才会映射
```javascript
function foo (a,b) {
   //arguments[10] 实参传几个就有几个，形参虽然有b但是没有传值，所以是undefined
   b = 99;
   console.log(arguments[1]);//undefined
}
foo (10);
```

javascript

### 特殊基本类型

+ undefined
    + 声明没有**赋值** 
