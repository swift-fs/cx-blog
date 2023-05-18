---
title: "Python专题 | Python异步编程"
description: ""
pubDatetime: 2023-04-14T18:00:00+08
postSlug: python-async
featured: false
draft: false
tags:
  - python
  - python专题
---

### 协程

协程不是计算机提供，程序员人为创造。协程也被称为微线程，是一种用户态的上下文切换技术。简而言之，其实就是通过一个线程实现代码块之间相互切换执行。

 实现协程的方式有很多种，但是目前只推荐使用**async，await关键字**实现协程。

#### 意义

在一个线程中如果遇到IO等待时间，线程不会傻傻等，利用空闲时间让线程去干点其他事。

### 事件循环

可以理解成一个死循环，去检测并执行某些代码。

```python
#伪代码
任务列表 = [任务1，任务2，任务3,...]
#事件循环
while True:
        可执行的任务列表，已完成的任务列表 = 去任务列表中检查所有的任务，将'可执行'和'已完成'的任务返回
        for 就绪任务 in 已准备就绪的任务列表:
                执行已就绪的任务
        for 已完成的任务 in 已完成的任务列表:
                在任务列表中移除已完成的任务

        如果任务列表中的任务都已完成,则终止循环 
```

```python
import asyncio

# 生成或者获取一个事件循环
loop = asyncio.get_event_loop()
# 任务添加到任务列表中，让事件循环去执行
loop.run_until_complete(任务)
```

### 简单例子

协程函数，定义函数时添加了关键字`async`。

协程对象， 协程函数调用会得到一个对象，就是协程对象。

```python
# 协程函数
async def a_func():
    pass


# 协程对象
a = a_func()
# <coroutine object a_func at 0x10bb0b530>
print(a)
```

 **注意：协程函数调用后，函数内部代码不会执行**

如果想要运行协程函数内部代码，必须要把协程对象交给事件循环处理:

```python
# 协程函数
import asyncio


async def a_func():
    print("协程执行了")


# 协程对象
a = a_func()
# <coroutine object a_func at 0x10bb0b530>
print(a)

# 老的写法
# loop = asyncio.get_event_loop()
# loop.run_until_complete(a)

# 新的写法 python3.7
asyncio.run(a)
```

### await

await后面只能跟可等待对象（协程对象，Future对象，Task对象，其实这三种对象目前可以理解为IO等待）。

例子1：

```python
import asyncio

async def func():
    print("协程开始执行")
    # 遇到await关键字（也就是IO等待），挂起当前协程（任务），等await结果返回时（IO结果返回），再继续往下执行。当协程挂起时，事件循环可以去执行其他协程任务
    response = await asyncio.sleep(2)
    print("协程执行完毕：", response)


asyncio.run(func())
```

 例子2：

```python
import asyncio


async def others():
    print("任务开始执行")
    await asyncio.sleep(2)
    print("任务执行结束")
    return '我是返回值'


async def func():
    print("协程开始执行")
    response = await others()
    print("协程执行完毕，结果为：", response)


asyncio.run(func())
```

例子3：

```python
import asyncio


async def others():
    print("任务开始执行")
    await asyncio.sleep(2)
    print("任务执行结束")
    return '我是返回值'


async def func():
    print("协程开始执行")
    response = await others()
    print("结果为：", response)
    response1 = await others()
    print("协程执行完毕，最终结果：", response1)


asyncio.run(func())
```

**await就是可等待对象得到结果后再继续向下执行**。上面的三个例子会感觉也没有提升程序性能啊，一碰到await就开始等待，那是因为此时事件循环里就这一个任务，没有其他任务可执行了，如果有其他任务，事件循环会去执行其他任务；其次，await只是让当前协程挂起，而且await的返回值，该协程后续也可能需要使用。

### Task对象

> Tasks用于并发调度协程，通过asyncio.create_task(协程对象)的方式创建Task对象，这样可以让协程立即 加入事件循环中等待被调度执行。除了使用 asyncio.create_task() 函数以外，还可以用低层级的 loop.create_task() 或 asyncio. ensure_future() 函数。不建议手动实例化 Task 对象。
>
> **本质上是将协程对象封装成task对象，并将协程立即加入事件循环，同时追踪协程的状态。**

大白话：在事件循环中添加多个任务。

```python
import asyncio


async def func(s: int):
    print("start")
    await asyncio.sleep(s)
    print("end")
    return f'返回值:{s}'


async def main():
    print("main 协程执行")
    # 创建Task对象，并且立即将func(1)协程包装成的任务添加到事件循环中
    task1 = asyncio.create_task(func(2))
    # 创建Task对象，并且立即将func(12协程包装成的任务添加到事件循环中
    task2 = asyncio.create_task(func(3))
    # main 协程碰到await挂起，事件循环就去执行其他任务，此时事件循环里还有task1，task2
    # 2s后task1执行完毕收到结果，3s后task2执行完毕收到结果，5s后下面的await收到结果
    await asyncio.sleep(5)
    # 在await asyncio.sleep(5)返回之前就已经有结果了，不用再等2s了
    t1 = await task1
    print(t1)
    # 在await asyncio.sleep(5)返回之前就已经有结果了，不用再等3s了
    t2 = await task2
    print(t2)


asyncio.run(main())
```

上面代码可以进行优化，如下：

```python
import asyncio


async def func(s: int):
    print("start")
    await asyncio.sleep(s)
    print("end")
    return f'返回值:{s}'


async def main():
    print("main 协程执行")

    task_list = [
        asyncio.create_task(func(2)),
        asyncio.create_task(func(3)),
    ]

    await asyncio.sleep(5)
    # 此处不能直接await task_list，因为不是可等待对象，需要包装一下
    result, pending = await asyncio.wait(task_list)
    print(result)


asyncio.run(main())
```

**注意：在`asyncio.create_task`之前，必须有事件循环存在。**

### Future对象

Task继承Future，await结果的处理就是基于Future对象来的。

例子1：

```python
import asyncio


async def main():
    loop = asyncio.get_event_loop()
    # 创建一个future对象，什么事情都不干
    fu = loop.create_future()
    # 等待future的最终结果，没有结果就会一直等待下去
    # 当前例子线程会一直阻塞等待结果
    r = await fu
    print("r:", r)


asyncio.run(main())
```

如果要想future返回结果，需要其他任务来设置fu结果返回：

```python
import asyncio


async def done(fu: asyncio.Future):
    await asyncio.sleep(3)
    fu.set_result("10089")


async def main():
    loop = asyncio.get_event_loop()
    fu = loop.create_future()
    # 3s之后会给fu设置结果，那么future就可以结束了
    await done(fu)
    r = await fu
    print("r:", r)


asyncio.run(main())
```