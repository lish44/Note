# 锁lock
--------

**lock 内部实现：**
- 关中断
- 缓存锁
- 总线锁


### 互斥锁

使用互斥锁能够保证同一时间有且只有一个thread进入临界区，其他的thread则在等待锁；当互斥锁释放后，等待的thread才可以获取锁进入临界区，
多个thread同时等待一个锁时，唤醒的策略是随机的。


### 读写锁

读锁
读多写少

写锁
写多读少

### 自旋锁

> 有一把谁抢到了谁就有执行权力 （每个人拿自己去交换唯一的，用完再交换回去）的锁。内部实现就是用了atomic_xchg 原子指令函数确保锁交换

缺点
每次lock都会引起cpu cache的同步 x86构架下 保证所有指令不能乱序
lock是一次原子操作 unlock也是一次
如果有两条线程争抢一把锁 必定会有一把锁抢不到 然后自旋 空转造成cpu浪费
拿到锁的线程有可能会被cpu切出去（因为cpu感知不到线程存在，取址
执行）所以可能会造成死锁


### 乐观派

主张 无锁 

**乐观锁不会被打断 悲观锁总是会打断**

cas保证 乐观锁

### 悲观派

主张 加锁

### CAS

> <font color=#bf616a>Compare And Swap</font> 

> <font color=#bf616a>lock cmpxchg</font>

表面是乐观锁 本质是悲观锁  cmpxchg 硬件保障 但不是atom 所以需要汇编层加lock 所以就变成了悲观

