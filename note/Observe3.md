#### 观察者模式.NET规范
--------

+ 两个接口Subject和Observer
```csharp
//.ENT命名规范 其实就是Subject
interface IObservable {
    void Register (IObserver obj);
    void Unregister (IObserver obj);
}
```
```csharp
interface IObserver {
    void Update (); //被subject调 以达到通知目的 - - 也就是等待被通知
}
```
--------

+ 用一个容器`container`来放IObserver的引用,也就是放对我感兴趣的对象（备胎列表）  
+ 以后再创建发布者（subject）直接继承这个基类就👌
```csharp
abstract class SubjectBase : IObservable {

    private List<IObserver> container = new List<IObserver> ();

    public void Register (IObserver obj) => container.Add (obj); //和下一句意义一样 语法糖

    public void Unregister (IObserver obj) { container.Add (obj); }

    protected virtual void Notify () {
        foreach (IObserver item in container) {
            item.Update ();
        }
    }
}
```
+ `Notify` 用于通知所有注册了的Observer的Update方法 - - 也就是发布通知 
--------
+ 发布者定义
```csharp
class Superstar : SubjectBase {
    private bool iscry;
    public bool Iscry { get { return iscry; } }

    public Superstar (bool b) { iscry = b; }

    public Superstar () : this (true) { }//为方便直接调构造

    //供子类覆盖，方便子类添加额外行为
    protected virtual void OnSend(){
        base.Notify();
    }

    //供对象调用
    public void PlayBall(){
        if (iscry)
            OnSend();
    }
}
```
--------

+ 订阅者定义
```csharp
class Fans : IObserver {
    public void Update () {
        System.Console.WriteLine ("这hmp又来装疯卖傻");
    }
}
```

+ main测试
```csharp
Superstar cxk = new Superstar ();//巨星
Fans f = new Fans ();//粉丝
cxk.Register (f);//粉丝订阅巨星
cxk.PlayBall ();//打球擦破皮哭了发个动态
```

