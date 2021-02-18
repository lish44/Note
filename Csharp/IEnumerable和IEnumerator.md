# IEnumerable 和 IEnumerator

### 迭代器
.NET 的迭代器其实就是通过这两个接口实现

#### IEnumerable 
源代码
```Csharp
public interface IEnumerable {
    IEnumerator GetEnumerator();
}
```
+ 其实就是一个接口 只有一个方法它就返回了 IEnumerator 这个接口

#### IEnumerator
源代码
```csharp
public interface IEnumerator {
    object Current { get; }
    bool MoveNext();
    void Reset();
}
```
其实也就一个属性两个方法

### 实现自己的迭代
```csharp
class SelfIEnumerable : IEnumerable {
    public IEnumerator GetEnumerator () {
        return new selfienumerator ();
    }
}
```
```csharp
class selfienumerator : ienumerator {
    int index = -1;
    string[] str = { "a", "b", "c", "d" };

    public object current => str[index];

    public bool movenext () {
        return ++index < str.length;
    }

    public void reset () {
        index = -1;
    }
}
```

<++>


