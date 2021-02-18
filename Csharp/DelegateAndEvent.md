# 委托和事件

### 委托

+ 概念 
    + 委托是种 **数据类型** - - 函数的数据类型，类似c++函数指针
    + 委托是一个类，它定义了方法的类型，能声明类的地方就能声明委托
+ 定义
    + `delegate` `<ReturnType>` `MethodNmae` `(parameterType)`;
    + 其中`<ReturnType>`- -返回值类型和`(parameterType)`- - 参数列表共同组成委托签名
    + 列如`delegate int Del (int a, int b);`

### 方法绑定到委托

定义一个委托
```csharp
delegate int Del (int a, int b);
```

定义一个方法 其中 **方法签名** 必须和 **委托签名** 一致
```csharp
static int Add (int a, int b) { return a + b; }
```

绑定方式1
```csharp
static void Main () {
    Foo foo;//声明委托变量
    foo = Add;//赋值
    var res = foo (3, 2);//像用方法一样使用委托 其实调用了Invoke方法
    System.Console.WriteLine (res);
}
```

绑定方式2
```csharp
Foo foo = new Foo (Add);//像初始化对象一样绑定
```

--------

### 多播

+ 可以将多个方法绑定到委托变量上用 `+=` 取消用`-=`

```csharp
namespace C_ {
	//定义委托类型Foo
    delegate int Foo (int a, int b);

    class Program {
        static int Add (int a, int b) {
            return a + b;
        }
        static int Sub (int a, int b) {
            return a - b;
        }
        static void Main () {
            /* 第一种方式
            Foo foo = new Foo (Add);
            foo += Sub;
            */
            Foo foo;//只是声明 未初始化
            foo = Add;//赋值
            System.Console.WriteLine (foo (3, 2));//输出5
            foo += Sub;
            System.Console.WriteLine (foo (3, 2));// 因为委托连所以输出1
        }
    }
}

```

+ 第一次用`=`是赋值，第二次用`+=` 是绑定，如果第一次就用`+=`会报**使用了未赋值的局部变量**

+ 委托必须先实例化以后，才能使用+=注册其他方法。如果对注册了函数的委托实例从新使用=号赋值，相当于是重新实例化了委托，之前在上面注册的函数和委托实例之间也不再产生任何关系

+ 委托编译后会生成一个继承自`MulticastDelegate`的类。`MulticastDelegate`继承自`Delegate`。`Delegate`内部维护了一个 **委托链表**
    + `GetInvocationList()`静态方法可以获取这个链表
------

### 事件
+ 定义
    + 封装委托变量 - - 为其量身定做的属性

实现
```csharp
namespace C_ {

    class MyEventTest {
        //event 关键字封装Action委托,Action是系统内置无参无返回委托类型
        public event System.Action ThisIsEvent;        
        public void Do () {
            if (ThisIsEvent != null)
                ThisIsEvent ();
        }
    }
    class Program {

        static void Foo () { System.Console.WriteLine ("Method::Foo"); }
        static void Foo2 () { System.Console.WriteLine ("Method::Foo2"); }
        static void Foo3 () { System.Console.WriteLine ("Method::Foo3"); }

        static void Main () {
            MyEventTest m = new MyEventTest ();

            m.ThisIsEvent += Foo;//更加人性化 不用再第一次=赋值 直接绑定
            m.ThisIsEvent += Foo2;
            m.ThisIsEvent += Foo3;
            m.ThisIsEvent -= Foo;
            //m.ThisIsEvent();//直接调用报错
            m.Do ();//实现了封装 用事件的发布者来调用

        }
    }
}
```

+ 用`event` 关键对委托进行封装，就像对字段用属性来封装一样

+ 对事件的声明，实际是声明一个私有委托变量 - - 所以👆倒数第二行报错
    + 为了更好的体现封装 可以把👆事件变为私有，用一个方法来进行绑定，也就是不用`m.ThisIsEvent += foo`用`m.Regist(foo)`在内部进行绑定


+ 此外事件内部还有两个方法`add_事件名`和`remove_事件名`分别对应`+=`和`-=`
    + 这个两个的访问权限取决声明事件时所用的访问限制符
    
    + `add`方法内部调用了`System.Delegate.Combine()`静态方法
        + 这个方法用于将当前变量添加到委托链表中
		+ 所以注册时就是按注册顺序添加进委托链表
		+ 所以当有返回值时，只能返回链表最后一个的值
------
### 事件访问器

```csharp
public class Test {
    //声明私有委托
    private Action action;
    
    //事件访问器
    public event Action Do{//只用于注册和取消注册使用
        add {action = value;}//只允许一个注册 
        remove{action -= value;}
    }
    
    public void DoSomeThing(){
        if (action != null)
            action();//通过委托变量调用
    }
}
//main
Test t = new Test();
t.Do += () => System.Console.WriteLine ("test");
t.Do += () => System.Console.WriteLine ("Rehma");//覆盖上一句
t.DoSomeThing();
```
--------
### Action 和 Func
系统内置委托类型直接用！不用自己定义了

[Action详解官方传送门](https://docs.microsoft.com/zh-cn/dotnet/api/system.action?view=netframework-4.8) 

[Func详解官方传送门](https://docs.microsoft.com/zh-cn/dotnet/api/system.func-1?view=netframework-4.8) 

### .ENT命名规范


委托名："**委托名EventHandler**"

委托原型定义一个`void`返回值，一个`Object`类型参数，一个`EventHandler`类型（或继承自EventArgs）

订阅事件的方法名："去掉**EventArgs**的委托名"

继承`EventAargs`的类型以`EventAargs`结尾

### 总结
使用委托可以将多个方法（签名相同）绑定到同一个委托变量，当调用此变量（用“调用”一词是因为此变量现在代表一个方法），就可以依次调用所有绑定的方法

