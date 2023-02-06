# 继承

## 继承修饰规则

| 继承权限  | public   | protected | private |
| :-:       | :-:      | :-:       | :-:     |
| public    | 公有     | 内部可用  | 不可用  |
| protected | 内部可用 | 内部可用  | 不可用  |
| private   | 不可用   | 不可用    | 不可用  |
> 当protected继承public属性时，继承过来的权限自动降级为protected,私有不变

## 继承后构造顺序
+ 有父类优先构造父类，编译器会在子类默认构造函数后隐式地在 **初始化列表** 添加父类默认构造，**只会**添加这默认构造
+ 既有父类又有包含对象，优先构造父类，其次包含对象，最后构造本类。同样编译器也会隐式地在**初始化列表**里添加对应的默认构造，
+ 先继承的先构造，最后构造子类自身
```c++
class D {
public:
    D(){cout<<"D cons"<<endl;}
    ~D(){cout<<"D des"<<endl;}
};
class A {
public:
    A(){cout<<"A cons"<<endl;}
    ~A(){cout<<"A des"<<endl;}
};
class B : public A {
public:
    B(){cout<<"B cons"<<endl;}
    ~B(){cout<<"B des"<<endl;}
};
class C : public B {
public:
    D d;
    C(){cout<<"C cons"<<endl;}
    ~C(){cout<<"C des"<<endl;}
};

void main () {
    C c;
}
/*输出结果
A cons
B cons
D cons
C cons
C des
D des
B des
A des
*/
```

## 子类的内存大小
+ 最大字节对齐
```c++
class A {
private:
    int m_a = 10;
public:
    short m_b = 20;
    void foo (){
        short m_c = 30;
    }
};
class B : A { //默认public继承? xcode上默认不写为private，应该和编译器有关
public:
    int m_d = 40;
};

void main () {
    cout << sizeof(A) << endl;// 8 -- short和当前最大字节int对其,4字节  
    cout << sizeof(B) << endl;// 12 -- B有m_a,m_b和m_c，都是独立于A的
}
```
> ⭐️小成员函数foo()存储在代码区，所以不占用对象空间

> ⭐️继承过来的属性、方法，独立与基类,方法其实本身就不在对象内
## 对象切割(object slicing)
```c++
class A {
private:
    int m_a = 10;
public:
    short m_b = 20;
    virtual void foo (){
        cout << "A" << endl;
    }
};
class B : public A {
public:
    int m_b = 40;
    void foo() override {//可以不写override关键字
        cout << "B" << endl;
    }
}

void main () {
    A a;
    B b;//因为继承 b包含a所有属性
    a = b;//b割舍自己部分,相当于把a那部分还给了a
    a.foo();//打印的是A
}
```
