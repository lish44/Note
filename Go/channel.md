### happens-before

1. 

> A send on a channel happens before the corresponding receive from that channel completes. 

对于一个have buffer channel, **send** happens-before **receive**， 可以说逻辑上send（`ch<-`）操作要优先于receive操作（`<-ch`）

2. 

> The closing of a channel happens before a receive that returns a zero value because the channel is closed. 

和 1 一样，只不过 ch<- 换成了 close(ch)，逻辑是一样的都是send，只不过recv的是channel的零值

3. 

> A receive from an unbuffered channel happens before the send on that channel completes. 

对于一个 no buffer channel, **receive** happens-before **send**，可以说逻辑上 receive（`<-ch`）操作要优先于 send（`ch<-`）

4. 

> The kth receive on a channel with capacity C happens before the k+Cth send from that channel completes.

也就是说，如果向buffer为n的channel，进行 send n+1 次操作，那么这次操作会block，Until one of them has been read from channel，也就是变成第3条，未满时就是第1条？

### 测试

go 启动后执行顺序无序，但有就近原则 一般是最后一个或者第一个优先执行? (至少测试是这样的结果，可能基数不够大？)


