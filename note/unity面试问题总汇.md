# 面试总汇
--------

### TCP和UDP 区别
他们都是TCP/IP协议族中 __传输层__ 的传输协议
#### TCP
+ 面向连接 面向字节流 可靠
+ 连接时三次握手 断开时四次挥手[]() 
+ 连接是点到点的连接
+ 收到数据保证顺序 有__拥塞控制__ __超时重发__ __丢弃重复数据__ __检验数据__ 等机制
#### UDP
+ 面向数据包 包头简单 速度快 不靠谱
+ 无需建立连接
+ 一对一，一对多，多对多，多对一发送
+ 没有拥塞 （网络拥塞也会继续发送）
https://mp.weixin.qq.com/s/KoRYNSRQjmYloI-YMBxTHQ

# 小公司面试题

### 天上友嘉
#### 数组里有{1，2，3，4，5，6，7}，随机打乱生成新的
```Csharp
public int[] RandomArray (int[] arr) {
    Random random = new Random ();
    for (int i = arr.Length - 1; i >= 0; i--) {
        int randomIndex = random.Next (0, arr.Length);
        int tmp = arr[i];
        arr[i] = arr[randomIndex];
        arr[randomIndex] = tmp;
    }
    return arr;
}
```

#### 判断一个整数是不是2的阶次方
```Csharp
public static bool Fun (int val) {
    return ((val & (val - 1)) == 0);
}
```

#### 通用排序
```Csharp
public class Sort<T> where T : IComparable {

    public void QuickSort (T[] arr, int l, int r) {
        if (l < r) {
            int low = l, high = r;
            T key = arr[l];
            
            while (low < high) {
                while (low < high && arr[high].CompareTo (key) >= 0) high--;
                Swap (ref arr[low], ref arr[high]);
                
                while (low < high && arr[low].CompareTo (key) <= 0) low++;
                Swap (ref arr[low], ref arr[high]);
            }
            
            QuickSort (arr, l, low - 1);
            QuickSort (arr, low + 1, r);
        }
    }

    public void Swap (ref T a, ref T b) {
        T tmp = a;
        a = b;
        b = tmp;
    }
}
```

#### 假设今日是2015年3月1日，星期日，算出13个月零6天后是星期几，距离现在多少秒
```Csharp
void CalculatorDay (int n) {
    int day = (n % 7);
}
```

#### 有两个篮子，分别为A和B，篮子A有鸡蛋，篮子B有苹果，用面向对象交换篮子的物品

# C#的
### QA:如何申明静态不可变量
```Csharp
static readonly int a = 10;
```

### QA:值类型引用类型和可空类型？区别是什么
+ 值类型继承自 System.ValueType 分配在 __线程堆栈__ 和 __托管堆__ 中，速度快
    - 结构体：struct（直接派生于System.ValueType）
        * 整 型：sbyte（System.SByte的别名），short（System.Int16），int（System.Int32），long （System.Int64），byte（System.Byte），ushort（System.UInt16），uint （System.UInt32），ulong（System.UInt64），char（System.Char） 
        * 浮点型：float（System.Single），double（System.Double）
        * 用于财务计算的高精度decimal型：decimal（System.Decimal）
        * bool型：bool（System.Boolean的别名）
    - 枚举：enum（派生于System.Enum）
    - 可空类型（派生于System.Nullable<T>泛型结构体，T?实际上是System.Nullable<T>的别名）
+ 引用类型继承自 System.Object 分配在 __托管堆__ 中，速度慢
    - 数组（派生于System.Array）
    - object（System.Object的别名）
    - 字符串：string（System.String的别名）
        * 类：class（派生于System.Object）
        * 接口：interface（接口不是一个“东西”，所以不存在派生于何处的问题。Anders在《C# Programming Language》中说，接口只是表示一种约定[contract]）
        * 委托：delegate（派生于System.Delegate）

[https://www.cnblogs.com/siqing99/archive/2012/04/03/2430918.html](https://www.cnblogs.com/siqing99/archive/2012/04/03/2430918.html) 
         
### QA:简述堆和栈

### QA:什么是GC？ 为什么要有GC？ 如何确保打开的文件正确关闭

### QA:泛型约束有那些?



### QA:虚函数（Virtual），抽象函数（abstract）和接口（interface）的区别
+ virtual：允许被重写，但不强制要求。声明时提供其自身实现；
+ abstract：强制要求其继承者重写。声明时不提供其自身的实现，抽象类不能被实例化；
+ interface：接口就是协议，其声明的成员（属性，方法，事件和索引器）必须由其继承的类实现。接口不能直接被实例化。

> 虚方法与抽象方法的区别在于，虚方法提供自身的实现，并且不强制要求子类重写；而抽象方法不提供自身的实现，并且强制子类重写。

> 抽象类与接口很相似，但是思路不一样。接口是公开类的成员，可多继承。而抽象类只能单继承。抽象更多用在关系紧密相关的类中，接口更多用于关系疏散但都有某一项功能的类中


