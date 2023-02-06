### 索引器
--------

#### 概念
让对象可以像数组一样被索引
```csharp
class Person {
    private string[] str = new string[3];
    public Person () {
        for (int i = 0; i < str.Length; i++) {
            str[i] = "测试文字" + i;
        }
    }
    public string this [int index] {
        get { return str[index]; }//可以先判断下index越界范围比较规范
        set { str[index] = value; }
    }
}
//main
Person p = new Person ();
System.Console.WriteLine (p[1]);//测试文字1
System.Console.WriteLine (p[2]);//测试文字2
```
+ public `<ReturnType>` `this` [ `<type>` name ] { }
    + `<ReturnType>`:返回类型
    + `this` 就是当前对象，固定写发
    + `[]` 就像重载运算符一样，使对象可以向数组访问
    + `<type>`:可以像数组一样用int当下标，也可以用string等其他类型

#### 接口实现
```csharp
interface Iindexer {
    int this [int index] {
        set;
        get;
    }
}
class A : Iindexer {
    private int[] arr = new int[] { 99, 88, 66 };
    public int this [int index] {
        get { return arr[index]; }
        set { arr[index] = value; }
    }
}
```
