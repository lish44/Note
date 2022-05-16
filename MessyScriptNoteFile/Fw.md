# 框架
--------

父节点可以引用子节点，子节点最后不用引用父节点

在unity中表现就是 子节点不要拖拽父节点到自己身上，最好在父节点里面引用子节点。

跨模块用事件，父类trigger 子类注册监听

怪物死亡 发送事件，管理怪物的父节点负责监听怪物的死亡，累计数量后做下一部操作

### 交互逻辑和业务逻辑
#### 交互逻辑
+ 在view中点击，造成model改变。 这个叫 <font color=#f4433c>交互逻辑</font>
+ view -> model 

#### 表现逻辑
+ model中的数据变更后，需要通知view显示，这个叫<font color=#f4433c>表现逻辑</font>
+ model -> view
![pic](https://raw.githubusercontent.com/lish44/pic/main/img/202205162220576.png)

