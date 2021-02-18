# const

### c和c++的const

+ 对于c,在局部是伪常量，会分配内存

```c
const int m_a = 10;
int* ptr = (int*)&m_a;

*ptr = 20;//可以修改
int arr[m_a];//报错 
```

+ 对于c++是真男人，不会分配内存，存在符号表里

```c++
const int m_a = 10;
int* ptr = (int*)&m_a;

*ptr = 20;      //不能修改
int arr[m_a];   //不报错 
```


+ c中const是默认外部链接,c++是内部

```c
//test.c
const int m_a;
//main
extern const int m_a;//告诉编译器m_a在外部
```
### const内存分配情况
+ 取地址 会分配临时内存
```c++
const int m_a = 10;
int* ptr = (int*)&m_a;//分配临时内存
```
编译器会做如以下操作
`int temp = m_a;`  temp有内存

`int* ptr = (int*)&temp;`  ptr指向临时空间 对ptr的操作都是对临时空间的

+ 加extern 会分配内存
```c++
extern const int m_a;
```

+ 用 **普通** 变量 初始化 const变量 会分配内存
```c++
int a = 10;
const int b = a;//分配内存
int* p = (int*)&b;
*p = 99;
cout<<b<<endl;//99
```
+ 自定义数据类型加const会分配内存（不常用）

### 引用和const 
+ 常量的引用 (reference to const)

    > 可以把引用绑定到const对象上，称为对常量的引用
    
    > 修饰的是 **引用对象** 不能变 或叫 **引用变量** 如👇`&c`

+ 可以用 **非常量** 或 **常量** 或 **字面值常量** 初始化 **常量引用**
```c++
int a = 10;
const int b = 20;

const int &c = a;   //非常量
const int &d = b;   //常量
const int &e = 30;  //字面值常量
//main
c = 40;//对b c d e都不能进行修改
```
+ 不可以用 **常量对象** 初始化 **非常量引用**
```c++
int &f = c;//报错--试图让非常量引用指向常量对象
```
### 指针和const
+ 指向常量的指针 (pointer to const)
    > 修饰的是指针 **所指的对象** 不能变
```c++
int a = 10, b = 20;
const int* ptr = &a;
//*ptr = 30;//❌--指向的对象不能被修改
ptr = &b;   //✔️--指针本身可以修改
cout<<*ptr; //20
```

+ 常量指针 (const pointer)
    > 修饰的是 **指针** 不能变
```c++
int a = 10, b = 20;
int *const ptr = &a;
*ptr = 30;  //✔️
ptr = &b;   //❌
```

+ 指向 **常量对象** 的 **常量指针**
    > 修饰的东西 全 不能改
```c++
int a = 10, b = 20;
const int* const ptr = &a;
*ptr = 30;  //❌
ptr = &b;   //❌
```



