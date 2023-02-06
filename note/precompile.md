# 预编译

## imply global暗示全局变量
+ 任何变量，未经声明就赋值，次变量为**全局对象** 所有
```javascript
 a = 10;//为全局window所有
 //window.a = 10;
 window{
    a : 10;
 }
```
## 一切声明的全局变量，全是window的属性
```javascript
var a = 10;//为全局window所有
//window.a = 10;
//window{
//a : 10;
//}
function foo () {
    var a = b = 10;
}
console.log(a);//undefined -- 范围在foo里面
console.log(b);//10 -- b未经声明就赋值属于全局window
```
> a在foo的AO里面

> b在全局GO里面
## 预编译在函数执行前一刻发生生成AO对象
```javascript
function fn(a) {
    console.log(a);
    var a = 123;//去AO对象里面的a赋值
    console.log(a);
    function a() { }
    console.log(a);
    var b = function () { }
    console.log(b);
    function d() { }
}
fn(1);
```
> 1.创建AO对象（执行期上下文）
```javascript
AO { }
```
> 2.找形参和变量声明,将变量和形参名作为AO属性名，值为undefined
```javascript
AO {
    a : undefined,
    b : underined,
}
```

> 3.将实参和形参统一(实参值放形参里面)
```javascript
AO {
    a : 1,
    b : underined,
}
```

> 4.在函数体里面找函数声明，值赋予函数体
```javascript
AO {
    a : function a(){ },
    b : underined,
    d : function d(){ }
}
```
> 5.创建完成后再执行函数
## 预编译发生在全局，生成GO（Global Object） === window
+ 和上面比少第三步



