# using 声明和编译指令

### using声明
    1.避免二义性 在局部声明后权限等级和被声明的对象权限一样 出现二义性
    2.写using声明后，以后代码都替换声明后的
```c++
namespace Test {
    int m_a = 10;
}

void main () {
    int m_a = 20;
    cout << m_a << endl;// 20 -- 就近原则
    
    using Test::m_a;//后面所有看到m_a都用Tset命名空间下的
    cout<< m_a << endl;//报错 二义性 因为有就近原则 需避免！
}
```

## using 编译指令
```c++
namespace Test {
    int m_a = 10;
}
void main () {
    int m_a = 20;
    cout << m_a << endl;// 20 -- 就近原则
    
    using namespace Test;//打开房间 
    cout << m_a << endl;// 20 --只是打开房间，用和不用自己选择
    cout << Test::m_a << endl;// 10; 
}

```

