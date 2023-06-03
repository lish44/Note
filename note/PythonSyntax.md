`__pycache__` 目录

是Python解释器在运行模块时自动生成的缓存文件目录，它用于存储模块的编译版本，可以提高模块的导入速度, 当我们导入一个模块时，Python会先检查是否有对应的.pyc文件存在, 此文件会在编译时生产,每个模块的.pyc文件都会保存在`__pycache__`目录中，以模块名和Python版本号命名

Generator 生成器
```python
from typing import Generator


def my_generator() -> Generator[int, str, str]:
    x = yield 88
    yield x.upper()


gen = my_generator()
num = next(gen)
print(num)
result = gen.send('foo')
print(result)
```
+ 主要是用来接应 yield返回的对象,是一个生成器函数,`-> Generator[int, str, str]:` 是函数注解,方便阅读,对返回类型其解释起解释作用,第一个参数是`int` 表示yield关键字右边返回值的类型, (e.g. num = next(iter) num的类型是int), 第二个参数是str表示send(str)发送的参数类型,第三个str表示return的类型
+ Generator[out,in,return] i.e. 参数类型的作用


async/await

```python
import asyncio


async def f1():
    print(1)
    await asyncio.sleep(2)
    print(2)


async def f2():
    print(3)
    await asyncio.sleep(2)
    print(4)

list = [
    asyncio.ensure_future(f1()),
    asyncio.ensure_future(f2())
]
lp = asyncio.get_event_loop()
lp.run_until_complete(asyncio.wait(list))
```
+ 要把一个函数通过协程方式运行,要标记async,然后遇到await就会塞住挂起,直到后面的逻辑返回才继续执行后面代码,这些协程函数需要统一丢到一个 **事件循环** 里面, 通过这个机制去轮训调用
+ await + IO等待 i.e. (其实有三种):
	+ 协程对象
	+ Future
	+ Task对象

协程对象:
```python
import asyncio


async def fn():
    print('fn start')
    await asyncio.sleep(2)
    print('fn end')
    return "fn over exit"


async def main():
    print('main runing ...')
    res = await fn()
    print(f'main finish... return {res} ')

asyncio.run(main())

# print ->:
"""
main runing ...
fn start
fn end
main finish... return fn over exit 
"""
```
+ main函数的返回值签名: `(function) def main() -> Coroutine[Any, Any, None]` 说明是个协程对象

Task对象
```python
import asyncio


async def fn(name, t):
    print(f'{name} start')
    await asyncio.sleep(t)
    return f"{name} finish ..."


async def main():
    print('main runing ...')
    event_loop_list = [
        asyncio.create_task(fn('f1', 1), name='f1'),
        asyncio.create_task(fn('f2', 2), name='f2')
    ]
    down, res = await asyncio.wait(event_loop_list)

    print(down)


asyncio.run(main())
```
+ asyncio.create_task : 把函数封装成对象,扔到事件循环里面




