# 观察者模式

### 委托事件实现

```csharp
using System;
using System.Collections.Generic;

namespace C_ {
    interface Subject {
        void Notify (string str);
        string SubjectState { get; set; }
    }

    //无返回值、一个参数 的委托事件
    delegate void EventHandler (string str);

    class Broker : Subject {
        public string SubjectState { get; set; }

        public event EventHandler Update; //事件

        
        /// <summary>
        ///通知订阅人 
        /// </summary>
        /// <param name="str">啥事</param>
        public void Notify (string str) {
            if (Update != null)
                Update (str);
            else
                System.Console.WriteLine ("没人关注老子通知个xx");
        }
    }

    class cxk {
        public void Dance (string str) {
            System.Console.WriteLine ("我蔡徐坤{0}了，跳锤子舞",str);
        }
    }

    class wyf {
        public void Rap (string str) {
            System.Console.WriteLine ("我skrrr。。{0}了，Rap个锤子",str);
        }
    }

    class qsh {
        public void daqian (string str) {
            System.Console.WriteLine ("我秦始皇在打钱，没空{0}",str);
        }

    }
}
```

main 测试
```csharp
Broker broker = new Broker ();

broker.Update += new EventHandler (new cxk ().Dance);
broker.Update += new EventHandler (new wyf ().Rap);
broker.Update += new EventHandler (new qsh ().daqian);

broker.Notify("吃大碗面");

//我蔡徐坤吃大碗面了，跳锤子舞
//我skrrr。。吃大碗面了，Rap个锤子
//我秦始皇在打钱，没空吃大碗面
```
