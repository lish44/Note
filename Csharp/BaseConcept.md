### 基本知识汇总

#### 装箱拆箱
+ 装箱
    + 在堆上为新生成的**对象实例** 分配内存，该对象实例包含数据，但没名字
    + 将栈上 值类型变量的值 赋值到 堆上的 对象中
    + 将堆上创建的对象的 **地址** 返回给引用类型变量（也叫对象引用）
    ```csharp
    int i = 1;
    Object boxed = i;//这里编译器自动完成上面三步
    ```
+ 拆箱
    + 获取以装箱的对象地址
    + 将值从**堆上**的对象中复制到**栈上**的 **值变量** 中
    ```csharp
    int j = (int)boxed;//显示声明拆箱类型
    ```
--------

+ 类不占内存，对象才占内存
--------

+ 继承构造函数问题  
    + 子类不继承父类构造函数
    + 子类默认调父类 **默认构造**  
        + 如果父类没有必须显示提供
        + `public A ():Base(){};` 调父构造
--------

#### 对象初始化器
```csharp
class Person {
	//自动属性
	public string Name { set; get; }
}
//main
Person p = new Person () { Name = "asd" };
```

#### as 和 is
__is 就是看它左边能不能兼容右边的，返回 bool ，不得抛异常__
+ 左边是儿子 右边是老子
+ 就是看有没得血缘关系，左边的一定是后代才有可能返回true

__as 就是直接转换，不能转换就返回空__ 
+ 儿子可以当（as）老汉，老汉不能当儿子。
+ 左边必须是儿子（和儿子的指针类型无关，和指向的空间才有关），右边必须是老子，才可能转换成功
+ 其实就是一般基类的属性少，子类的比较多，基类如果转过去了之后，有些子类东西它莫得，所以莫法转换

```Csharp
public interface ITest {
    void Notice ();
}

public class Father {
    public virtual void Notice () {
        System.Console.WriteLine ("F yes");
    }
}

public class A : Father, ITest {
    public override void Notice () {
        System.Console.WriteLine ("A yes");
    }
}
public class B : A, ITest {
    public new void Notice () {
        System.Console.WriteLine ("B yes");
    }
}

class Program {
    static void Main (string[] args) {
        A a = new A ();
        Father f = new A ();
        Father ff = new B ();
        //== is == 
        bool a1 = a is Father; // true a:Father
        bool f1 = f is Father; // true 老子的指针指向的儿子的空间，
        bool ff1 = ff is Father; // true 同上
        a.Notice (); // A
        f.Notice (); // A
        ff.Notice (); // A 如果是override 就是 B

        bool a2 = a is ITest; //true
        bool a3 = a is B; // false
        bool f2 = f is ITest; // true
        bool f3 = f is A; // true f现在指的是A空间 所以 可转换成 A
        bool f4 = f is B; // false B是A的儿子

        System.Console.WriteLine (f4);
        //========
    }
}
```

<++>


