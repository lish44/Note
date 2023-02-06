# 泛型
--------
### 泛型约束

| 约束类型            | 含义                                                     | 实例代码              |
| :-:                 | :-:                                                      | :-:                   |
| where T: `struct`   | T只能为值类型（除nullable）                              | [走起](#值类型约束)   |
| where T: `class`    | T只能为引用类型                                          | [走起](#引用类型约束) |
| where T: `new()`    | 必须有公共的无参构造函数（和其他约束一起时，必须放最后） | [走起](#new()约束)    |
| where T: `<基类名>` | T只能为约束中的基类，或基类的派生类型                    | [走起](#基类类约束)   |
| where T: `<接口名>` | T只能为 继承过限定的接口                                 | [走起](#接口约束)     |
##### 值类型约束 

```csharp
class Book<T> where T : struct {
    T price;
    T id;
}
//main
Book<int> book = new Book<int> ();
book.price = 99;
book.id = 1;
//Book<string> book = new Book<string> ();//❗️报错
```

##### 引用类型约束 
```csharp
class Book<T> where T : class{ public T name; }
//main
//Book<int> book = new Book<int> ();//❗️
Book<string> book = new Book<string> ();
book.name = "一的法则";
```

##### new()约束 

```csharp
class MyString {
    public MyString () { }
    public string str;
}

class Book<T1, T2> where T1 : class, new () where T2 : struct {
    public T1 name;
    public T2 price;
}

//main
// Book<string, int> book = new Book<string, int> ();//❗️
Book<MyString, int> book = new Book<MyString, int> ();
book.name.str = "一的法则";
book.price = 369;
```
+ 这个new()必须写在最后，且作用只是为了检查 **约束的类型** 是否有 **公共无参构造函数**

##### 基类类约束 
```csharp
abstract class SeniorAnimal{//高级动物 基类
    public abstract void Speak();
}
class person : SeniorAnimal {//人类 子类
    public override void Speak () {
        throw new NotImplementedException ();
    }
}
class cat { }

//指定泛型参数 必须派生于基类 SeniorAnimal
class Test<T> where T : SeniorAnimal {
    //CODE...
}

//main
Test<person> t = new Test<person>();
//Test<cat> t = new Test<cat>();//❗️
```

##### 接口约束 
```csharp
//吃饭接口
interface IEat { void Eat (); }

//限定泛型参数必须实现 IEat这个接口
class Test<T> where T : IEat { }

//继承了吃这个接口
class Person : IEat {
    public void Eat () { }
}

//它很厉害 不用吃饭
class CXK { }

//main
Test<Person> p = new Test<Person> ();
// Test<CXK> p = new Test<CXK>();//❗️
```

