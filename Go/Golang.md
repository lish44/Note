# Go 基本语法

--------

### 类型

int 

string 

uint32

uint64

#### channel

> 在go中 goroutine 的交流途径用 **channel** 来实现

> <font color=#bf616a>Don't conmmunicate by sharing memory; share memory by communicating</font>

> 交流是双向的 发消息和收消息都会阻塞代码，<font color=#bf616a>直到对方接收到</font>

创建

`ch := make(chan string)` 

- 带数据类型

读写ex:

```go
func main() {
	// 创建无缓存channel
	ch := make(chan string)
	go huahua(5, "🤡", ch)

	// 自旋等待接收
	for {
		// 读操作 如果没有写操作这里会一直读造成死锁，这个deadlock并不是 for 引发的而是channel读写的自身阻塞
		msg, err := <-ch
		if !err {
			break
		}
		fmt.Println(msg)
	}

	// 简写
	// for msg := range ch {
	// 	fmt.Println(msg)
	// }
	fmt.Println("====== main func exit ======")
}

func huahua(n int, str string, ch chan string) {
	defer close(ch)
	for i := 0; i < n; i++ {
		// 写操作
		ch <- str
		time.Sleep(time.Millisecond * 500)
	}
}
```
- channel 的读写需要对应
- defer 保证函数在出栈前最后一刻执行
- close(ch) 每个channel需要保证退出，不然会造成死锁 

简单的读写死锁案例ex:

```go
func main() {
	ch <- "test"// 写
	msg := <- ch// 读
	fmt.Println(msg)
	close(ch)
}
```
- ch 没有缓存能力，在第一行进行写操作时代码会阻塞，会等待一个对应的读操作，而读操作在下一行，逻辑上永远等不到，所以造成死锁。
- 如果一二行交换 先读后写，情况也一样。因为没有写而无法读，造成死锁。
- 解决办法简单 就是开两条线程并发读写

```go

func main() {
	ch := make(chan string, 0)

	go func() {
		ch <- "test"
	}()

	go func() {
		// range会自动检测关闭channel
		for msg := range ch {
			fmt.Println(msg)
		}
	}()

	time.Sleep(time.Millisecond * 1) // 如果不写这句，main函数的goroutine结束后，所有grt都会结束
	
	/** 或者直接让读在main里直接跑起来
	ch := make(chan string)
	go func() {
		ch <- "test"
		close(ch)
	}()
	for msg := range ch {
		fmt.Println(msg)
	}
	*/

}
```
- 这里grt还没起起来程序就结束了?



### 异步

##### 使用 sync.WaitGroup 计数管理

```Go
func main() {
	var wg sync.WaitGroup
	wg.Add(2)

	// 匿名函数+立即执行
	go func() {
		huahua(3, "👻")
		// huahua 执行完成后 计数器-1
		wg.Done()
	}()

	go func() {
		huahua(3, "🤡")
		wg.Done()
	}()

	wg.Wait()// 阻塞

	fmt.Println("====== main func exit ======")
}

// print func
func huahua(n int, str string) {
	for i := 0; i < n; i++ {
		fmt.Println(i+1, ": ", str)
		time.Sleep(time.Millisecond * 500)
	}
}
```

- `wg.Add()` 添加计数个数
- `wg.Wait()` 程序阻塞 等待计数器为0 恢复执行 , wg 要确保goroutine 执行完成不然会出现 **deadlock**
- `wg.Done()` 计数-1

