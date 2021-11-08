# 命令模式 CommandPatterns
--------

解决三个问题 
1. 按键匹配
2. 输入撤销
3. 

### 实现
首先要一个命令接口CommandInterface (也可以是抽象类 总之要子类继承了可以强制重写)
```Csharp
public abstract class Command
{
    protected float moveDistance = 1f;
    public abstract void Execute(Transform boxTrans, Command command);
    public virtual void Undo(Transform boxTrans) { }
    public virtual void Move(Transform boxTrans) { }
}
```
+ Execute 就是子类继承后统一调用的方法
+ Undo 就是撤销操作的统一接口
+ Move 就是移动操作的统一接口，（可以不写 看需求）

然后实现具体的命令类，一个命令就是一个类，必须继承Command接口，因为要调用Execute
```Csharp
public class MoveForward : Command
{
    public override void Execute(Transform boxTrans, Command command)
    {
        Move(boxTrans);

        InputHandler.oldCommands.Add(command);
    }

    public override void Undo(Transform boxTrans)
    {
        boxTrans.Translate(-boxTrans.forward * moveDistance);
    }

    public override void Move(Transform boxTrans)
    {
        boxTrans.Translate(boxTrans.forward * moveDistance);
    }
}
```
+ 继承后的 Execute 就是具体的这个命令类的实现
+ InputHandler.oldCommands 是个全局变量，类型是 `List<Command>`，用来记录本次操作的指令
+ Undo 就是反向操作，比如这个命令是往前走，对应的撤销就是回来，就是往后退
+ Move 可有可无，有的话统一了写法比较正规

往后走的命令类 同上
```Csharp
public class MoveReverse : Command
{
    public override void Execute(Transform boxTrans, Command command)
    {
        Move(boxTrans);
        InputHandler.oldCommands.Add(command);
    }

    public override void Undo(Transform boxTrans)
    {
        boxTrans.Translate(boxTrans.forward * moveDistance);
    }

    public override void Move(Transform boxTrans)
    {
        boxTrans.Translate(-boxTrans.forward * moveDistance);
    }
}
```


