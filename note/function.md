# 函数

## 指针作为函数参数

+ 在调用时
+ 实参将以 **值** 传递给形参 (压栈 函数执行完后出栈）
+ 实参形参地址**相同** ,指向同一空间
+ 形参改变会影响实参指针所指向的数据值

## this指针
+ 会默认在构造函数参数列表里添加
```c++
class A {
public:
    int m_a = 10;
    A (/* A* this, */int m_a){//编译器自动添加this，谁调用this就指向谁
        this->m_a = m_a;
    }
};

void main () {
    A a1(99);//此时this指向a1对象，a1对象的地址赋值给了this指针,this = &a1。
}
```
+ 返回对象本身
```c++
A& foo (int m_a) {
    this->m_a += m_a;
    return *this;
}
```
> this指向调用者，*this代表调用者本身，返回值为类型引用（可以.出来，返回后当对象使用，此时返回的是调用者本身）

## 指针函数
+ 返回 **指针** 的 函数 （是个函数！）
> 可以用作于返回数组某一位
```c++
int arr[]{1,2,3};
int* foo (int* ptr){
    return &ptr[2];
}
//main
cout << *foo(arr);// 3
```

## 函数指针
+ 指向 **函数** 的 指针 (是个指针！）
    > 程序编译时，函数都有个入口，每次调用函数就会找这个入口，入口就是个地址，函数指针就是存的这个地址

+ 形式
    > `ret (*ptr)(args,args1,...);`

    > `ret` 代表返回值类型

    > `(*ptr)` 指针名，是个整体，代表指向某个函数

    > `(args,args1,...)` 形参列表
```c++
int foo (int a, int b) { reutrn a + b; }

void main () {
    //函数指针的签名必须和指向的函数签名相同
    
    int (*ptr)(int,int);        // int--返回类型 （*ptr）--指向函数的指针 （int,int）-- 参数的类型匹配
    
    //int (*ptr)(int,int) = foo;//下三行等价
    //ptr = foo;                //对函数名取地址和使用函数名一样的
    ptr = &foo;
    
    cout << (*ptr)(10,20);      // 打印30
    cout << foo(10,20);         // 和上行等价，函数名被编译或其实就是地址
}
```

## 函数指针数组
+ 存 **函数指针** 的 数组
    > `ret (*ptr[c])(args,args1,...);` 和👆差不多，只不过多个`[c]`,ptr从指针变成数组
    
    > `[c]` 其中c代表数组容量
    ```c++
    //ptr是数组名，数组大小为2。（int，int）函数参数列表。int代表函数返回值
    int (*ptr[2])(int,int);

    int Add (int a, int b){ return a + b; }
    int Sub (int a, int b){ return a - b; }
    
    ptr[0] = Add;//通过这个表达式，把函数的地址赋值给数组第一位
    ptr[1] = &Sub;//与上行等价
    
    cout << ptr[0](10,20) << endl;      //等价(*ptr)(10,20)
    cout << (*(ptr+1))(99,1) << endl;   //等价ptr[1](99,1)
    ```
    初始化列表
    
    `int (*ptr[2])(int,int){Add,Div};` 和👆赋值等价
## 回调函数
+ 将函数作为参数
```c++
int Add (int a, int b){ return a + b; }
int Sub (int a, int b){ return a - b; }

int CallBack(int a, int b, int (*ptr)(int,int)){ 

    return ptr(a,b);
}
//main
cout << CallBack(20, 10, Add);// 打印30
cout << CallBack(20, 10, Sub);// 打印10
```

## 绕过private控制权限
```c++
class A {
private:
    int m_a = 10
    int m_b = 20;
public:
    int Getm_a(){ return m_a; }
    int Getm_b(){ return m_b; }
};
//main
A a;
*((int*)&a) = 99;           //m_a赋值为99
((int*)&a)[0] = 88;         //m_a赋值为88
cout << a.Getm_a() << endl; //88

*(((int*)&a) + 1) = 77;     //m_b赋值为77
((int*)&a)[1] = 66;         //m_b赋值为66
cout << a.Getm_b() << endl; //66
```
> `*((int*)&a)` 解析

> `&a` 函数指针

> `(int*)&a` 强转为4字节寻址空间的指针,现在指针存的地址是第一个变量m_a的地址

>`*( (int*)&a )` 解引用后，现在代表m_a实际内容

> 所以`((int*)&a)[0]`等价`*((int*)&a)` 

> `((int*)&a)[0]` 可以理解为`ptr[0]`,ptr就是指针，因为是指针所以也可以当做数组来用，数组第一位存的就是m_a，第二位存的就是m_b;

## 函数名是地址码 - - 不是
> 函数名并不是函数地址的代表，这种误解与数组名就是指针一样犯了相同的错误。函数名是函数实体的代表，不是地址的代表，当然，你马上就会有疑问，平时我们不都是把函数名作为函数的地址吗？是的，我可以告诉你，函数名可以作为函数的地址，但是，绝大多数人都忽略了一个条件，从函数到指针的隐式转换是函数名 **在表达式中** 的行为，就是说，这个转换仅在表达式中才会发生，这仅是函数名众多性质中的一个，而非本质，函数名的本质就是函数实体的代表。

> 到了C++，由于C++规定，非静态成员函数的左值不可获得，因此非静态成员函数不存在隐式左值转换，即不存在像常规函数那样的从函数到指针的隐式转换，所以必须在非静态成员函数前使用&操作符才能获得地址。

链接：https://www.jianshu.com/p/215bef2208c7

# 函数参数

> 当函数无需修改引用形参的值时，最好声明成常量引用
--------
### 数组形参
+ 标准库规范
```c++
void Print (const int* begin, const int* end){
    while (begin != end)
        cout<< *begin++ <<endl;
}
//main
int arr[]{1,2,3};
Print(begin(arr), end(arr));

auto len = end(arr) - begin(arr);//3 
```
> `begin` 返回指向首元素的指针

> `end` 返回指向尾元素的下一个元素的指针

>`len` 类型是`ptrdiff_t` 和 `size_t` 一样是一种标准库类型，定义在cstddef头文件中，是一种和机器相关的类型

+ 数组引用形参
```c++
void Print(int (&arr)[3]) {//限制了数组大必须为3
    for(auto temp : arr){
        cout << temp <<endl;
    }
}
```
> 必须加`( )`，如果不加就把arr声明成了引用的数组 

# 函数返回值
> 返回一个值的方式，和初始化一个变量或形参一模一样

> 返回的值用于初始化调用点的一个临时量，该零时量就是调用结果




