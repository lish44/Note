# 命令模式 CommandPatterns
--------

解决问题 
1. 按键匹配
2. 输入撤销

### 实现
首先要一个命令接口CommandInterface (也可以是抽象类 总之要子类继承了可以强制重写)
```Csharp
using System;
using System.Collections.Generic;

namespace Patterns
{
    // 命令接口子命令类继承后用来统一调用
    public interface ICommand
    {
        void Execute();
        void Unod();
    }
    
    // 移动命令单独一个类封装
    class MoveCommand : ICommand
    {
        public void Execute()
        {
            System.Console.WriteLine("移动");
        }

        public void Unod()
        {
            System.Console.WriteLine("撤销移动");
        }
    }

    class FlyCommand : ICommand
    {
        public void Execute()
        {
            System.Console.WriteLine("飞");
        }

        public void Unod()
        {
            System.Console.WriteLine("撤销飞");
        }
    }

    // 命令的调用的执行者 不需要晓得命令是干啥的 只需要根据传过来的命令执行就行，简单封装了一些操作
    class Invoker
    {
        Stack<ICommand> undoCommands = new Stack<ICommand>();
        Stack<ICommand> redoCommands = new Stack<ICommand>();

        // 主要就是这个方法 传什么命令 执行什么命令（让命令参数化）
        // 后期拓展还可以加参数，具体到某个对象，比如role，然后判断_command 执行对应role的命令
        void ExecuteCommand(ICommand _command)
        {
            _command.Execute();
            undoCommands.Push(_command);
            redoCommands.Clear();
        }

        void Undo()
        {
            if (undoCommands.Count <= 0)
            {
                System.Console.WriteLine("没有撤销命令");
                return;
            }

            var command = undoCommands.Pop();

            command.Unod();

            redoCommands.Push(command);
        }

        void Redo()
        {
            if (redoCommands.Count <= 0)
            {
                System.Console.WriteLine("没有反撤销命令");
                return;
            }

            var command = redoCommands.Pop();

            command.Execute();

            undoCommands.Push(command);
        }
        
        // 按键绑定的更换 只需要传两个按键的引用就可以交换
        void Swap(ref ICommand a, ref ICommand b)
        {
            var tmp = a;
            a = b;
            b = tmp;
        }

        void Play()
        {
            var cmd = undoCommands.ToArray();
            for (int i = cmd.Length - 1; i >= 0; i--)
            {
                cmd[i].Execute();
            }
        }
        
        // 这里是客户端代码 用来演示
        public void Go()
        {
            ICommand btn1, btn2;

            btn1 = new MoveCommand();
            btn2 = new FlyCommand();

            string str = string.Empty;
            while (true)
            {
                str = Console.ReadLine();
                if (str.Equals("1")) ExecuteCommand(btn1);
                if (str.Equals("2")) ExecuteCommand(btn2);
                if (str.Equals("z")) Undo();
                if (str.Equals("r")) Redo();
                if (str.Equals("c")) Swap(ref btn1, ref btn2);
                if (str.Equals("p")) Play();
                if (str.Equals("q")) return;
                System.Console.WriteLine("=============");
            }

        }
    }

}
```
+ Execute 就是子类继承后统一调用的方法
+ Undo 就是撤销操作的统一接口
+ 然后实现具体的命令类，一个命令就是一个类，必须继承Command接口，因为要调用Execute
 
 
__参考链接__ 

+ [https://refactoringguru.cn/design-patterns/command/csharp/example#lang-features](https://refactoringguru.cn/design-patterns/command/csharp/example#lang-features) 
+ [https://www.cnblogs.com/tangyikejun/p/5931571.html](https://www.cnblogs.com/tangyikejun/p/5931571.html) 
+ [https://github.dev/Habrador/Unity-Programming-Patterns](https://github.dev/Habrador/Unity-Programming-Patterns)
+ [https://gpp.tkchu.me/command.html](https://gpp.tkchu.me/command.html)
