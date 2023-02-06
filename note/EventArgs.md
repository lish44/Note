# EventArgs
--------

### 理解
本质就是一个规范，就是所有需要传递的数据类型都继承EventArgs这个类，通过这个类就说明了这是一个附带信息。

### 列子
```Csharp
namespace Main {
    class Program {
        static void Main (string[] args) {
            Counter c = new Counter ();
            c.handler += c_ThresholdReached;
            c.Go ();
        }

        static void c_ThresholdReached (object sender, CustomEventArgs e) {
            var t = sender.GetType ();
            System.Console.WriteLine (t.Name);
            Console.WriteLine ("{0} ", e.TimeReached);
            Environment.Exit (0);
        }
    }

    class Counter {
        public event EventHandler<CustomEventArgs> handler;
        public void Go () {
            CustomEventArgs args = new CustomEventArgs ();
            args.TimeReached = DateTime.Now;
            if (handler != null) {
                handler (this, args);
            }
        }
    }

    public class CustomEventArgs : EventArgs {
        public DateTime TimeReached { get; set; }
    }
}
```
+ CustomEventArgs 类就是附带信息类继承了EventArgs，其实不继承也行 就是因为<font color=#f4433c>规范</font> 

+ EventHandler<T> 是一个.ENT 封装好了的委托 `public delegate void EventHandler<TEventArgs>(object? sender, TEventArgs e);` 通过泛型T 确定了附带信息类的类型，减免了开箱的消耗

+ handler传this就是说明了这个事件的调用者是谁发起的

原文：[https://docs.microsoft.com/zh-cn/dotnet/api/system.eventhandler-1?view=net-5.0](https://docs.microsoft.com/zh-cn/dotnet/api/system.eventhandler-1?view=net-5.0) 
