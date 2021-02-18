# namespace命名空间

## 解决命名冲突

+ 头文件A.h
    ```c++
    
    namespace TestA {
        void foo();
    }
    ```

+ 主文件A.cpp
    ```c++
    #include"A.h"
    foo(){
        cout << "A foo method" << endl;
    }
    ```
+ 头文件B.h
    ```c++
    namespace TestB {
        void foo();
    }
    ```

+ 主文件B.cpp
    ```c++
    #include"B.h"
    foo(){
        cout << "B foo method" << endl;
    }
    ```

+ main
    ```c++
    #include"A.h"
    #include"B.h"
    
    TestA::foo();
    TestB::foo();
    ```

## 基本要求

    1.必须定义在全局作用于下
    2.可以放函数、变量、结构、类
    3.可以嵌套
    4.开放的，可以随时添加内容
```c++
namespace Test {
    int m_a = 10;
    void Foo();
    struct Person();
    class Animal();
    namespace Test2 {
        int m_a = 20;
    }
}
//两个Test会进行合并，不会覆盖
namespace Test {
    int m_b = 99;
}

void main (){
    //输出Test2下的m_a
    cout << Test::Test2::m_a << endl;
}
```
## 匿名空间
+ 相当于静态，只在当前文件范围有效
```c++
namespace {
    int m_a = 10;//static int m_a = 10;
    int m_b = 20;//static int m_b = 20;

}
```

## 起别名
```c++
namespace ThisIsVeryLongNamespace {
    int m_a = 10;
}

void main () {
    namespace fine = ThisIsVeryLongNamespace;
    cout << fine::m_a << endl;
    cout << ThisIsVeryLongNamespace::m_a << endl;
}
```

