---
title: "Python标准库 | functools模块"
description: "functools模块应用于高阶函数，即参数或（和）返回值为其他函数的函数。大白话就是：一个函数的参数是函数类型，那么是高阶函数；一个函数的返回值是函数类型，那么是高阶函数；那么两者都有，肯定也是高阶函数。 "
pubDatetime: 2023-04-11T18:00:00+08
postSlug: python-functools
featured: false
draft: false
tags:
  - python
  - python标准库
---

### reduce函数

reduce函数将两个参数的 function 从左至右积累地应用到 iterable 的条目，以便将该可迭代对象缩减为单一的值。它的语法是：`functools.reduce(function, iterable[, initializer])`。可以理解为 reduce 中的第一个参数 function 是一个函数，它有两个变量（function 的变量），iterable 是一个序列，function 第一次执行时，按顺序先取两个传入执行，得到一个结果，然后再将这个结果与 iterable 中的下一个值（还是两个变量）传入 function 执行，如此反复直到 iterable 里的值取完为止，最终就能得到一个终极的返回值。

如果存在可选项 initializer，它会被放在参与计算的可迭代对象的条目之前，并在可迭代对象为空时作为默认值。 如果没有给出 initializer 并且 iterable 仅包含一个条目，则将返回第一项。

```python
import functools


def sum001(a, b):
    # 第一次调用，a=0，b=l1[0]
    # 第二次调用, a=0+l1[0]['age],b=l1[1]
    # 第三次调用, a=0+l1[0]['age]+l1[1]['age],b=l1[2]
    # ...
    # 最终结果为单一值
    return a + b['age']


l1 = [
    {
        "name": "呵呵",
        "age": 10,
    },
    {
        "name": "哈哈",
        "age": 11,
    },
    {
        "name": "嘿嘿",
        "age": 7,
    },
    {
        "name": "嘿嘿",
        "age": 60,
    }
]

r1 = functools.reduce(sum001, l1, 0)
print(r1)
```

#### initializer 参数

指定 initializer 参数时，第一次执行时，函数的第一个参数传入此值，第二个参数为序列的第一个值；当序列为空时，则返回就是 initializer 的值；如果 initializer 没有指定，序列也会空，则会报错。**所以，任何时候都强烈建议传入一个初始值。**

### lru_cache函数

lru_cache 是一个为函数提供缓存功能的装饰器，在下次以相同参数调用时直接返回上一次的结果。用以节约高开销或 I/O 函数的调用时间。

它实现了 最近最少使用（Least-recently-used）缓存装饰器，缓存函数的参数必须是可哈希的。最近最少使用的机制是如果一个数据在最近一段时间没有被访问到，那么在将来它被访问的可能性也很小， LRU算法选择将最近最少使用的数据淘汰，保留那些经常被命中的数据。

以下是它的几个参数的说明：

- user_function：如果指定，它必须是一个可调用对象
- maxsize：存储在缓存中的元素数，默认 128个，如果设为 None，LRU 特性将被禁用且缓存可无限增长
- typed：布尔值，默认为 Flase
  - 如果 typed 被设为真值，则不同类型的函数参数将被分别缓存。 例如，f(3) 和 f(3.0) 将总是会被当作具有不同结果的不同调用。
  - 如果 typed 为假值，则具体实现通常会把它们当作相同调用并且只缓存一个结果，虽然并不一定总是会这样做。

被装饰的函数会成为 `functools._lru_cache_wrapper` 对象，它有以下属性和方法：

- `f.cache_parameters()`：缓存参数
- `f.cache_info()`：当前缓存情况，返回一个 namedtuple，包含缓存使用、未使用、长度、最大长度，如 CacheInfo(hits=2, misses=1, maxsize=128, currsize=1)
- `f.cache_clear()`：清除缓存
- `f.__wrapped__()`：未被装饰的参数

```python
from functools import lru_cache


@lru_cache
def count_vowels(sentence):
    return sum(sentence.count(vowel) for vowel in 'AEIOUaeiou')


print(count_vowels)
# <functools._lru_cache_wrapper at 0x102f33530>

# 缓存参数
print(count_vowels.cache_parameters())
# {'maxsize': 128, 'typed': False}

# 缓存信息初始量
print(count_vowels.cache_info())
# CacheInfo(hits=0, misses=0, maxsize=128, currsize=0)

# 执行3次
# 函数执行
count_vowels('hello')
# 直接从缓存中取值
count_vowels('hello')
# 直接冲缓存中取值
count_vowels('hello')

# 缓存被使用两次，一次没用（第一次执行时），大小为 1
print(count_vowels.cache_info())
# CacheInfo(hits=2, misses=1, maxsize=128, currsize=1)

# 清除缓存
count_vowels.cache_clear()
# 无返回 None

# 再看看缓存情况
print(count_vowels.cache_info())
# CacheInfo(hits=0, misses=0, maxsize=128, currsize=0)
```

**注意点：lru_cache 以及 cache 应该作用于纯函数。**

### 延伸：纯函数

> 相同的输入，总是会的到相同的输出，并且在执行过程中没有任何副作用。

该怎么去理解上面的概念呢？我们要把上面这句话拆成两部分来看。

#### 相同的输入，总是会得到相同的输出

```python
a = 1


def x_add(x):
    return x + a


x_add(1)

```

上面这个函数就不是一个纯函数，因为在我们程序执行的过程中，变量`a`很可能会发生改变，当变量a发生改变时，我们同样执行`x_add(1)`时得到的输出也就不同了。

改造后：

```python
def x_add(x, y):
    return x + y


x_add(10, 20)
```

符合相同的输入得到相同的输出这个概念。

#### 执行过程中没有任何副作用

这里我们要搞清楚什么是副作用，这里的副作用指的是函数在执行过程中产生了**外部可观察变化**。

1. 发起HTTP请求
2. 修改外部数据
3. 打印数据

上面一系列操作都可以被称为是副作用。下面可以接着看一个修改外部数据从而产生副作用的例子：

```python
a = 10


def f(x):
    global a
    a = x


f(109)
print(a)

```

我们运行了`f`函数，外部的变量`a`的值发生了改变，这就是产生了所谓的副作用，所以`f`不是一个纯函数。当我们这样进行修改：

```python
a = 10


def f(x):
    # global a
    a = x


f(109)
print(a)
```

修改后的函数`f`不会对产生外部可观察变化，也就不会产生副作用，它就是一个纯函数。

一个纯函数，上面所说的两个条件缺一不可。

通过了解纯函数的概念，我相信有的小伙伴已经能感觉到纯函数的一些的好处了：

- 更容易进行测试，结果只依赖输入，测试时可以确保输出稳定
- 更容易维护和重构，我们可以写出质量更高的代码
- 更容易调用，我们不用担心函数会有什么副作用
- **结果可以缓存，因为相同的输入总是会得到相同的输出（和刚提到的lru_cache进行结果缓存正好一致）**

### wraps函数

Python 装饰器（decorator）在实现的时候，被装饰后的函数其实已经是另外一个函数了（函数名等函数属性会发生改变），为了不受影响，Python 的 functools 包中提供了一个 @wraps 的装饰器来消除这样的副作用。写一个 decorator 的时候，最好在实现之前加上 functools 的 wrap，它能保留原有函数的名称和 docstring。

```python
from functools import wraps


def my_decorator(f):
    @wraps(f)
    def wrapper(*args, **kwargs):
        print('Calling decorated function')
        return f(*args, **kwargs)

    return wrapper


@my_decorator
def example():
    """Docstring"""
    print('Called example function')


example()
# Calling decorated function
print(example.__name__)
# 'example'
print(example.__doc__)
# 'Docstring'
```

### cached_property

Python 内置模块 functools 提供的高阶函数 `@functools.cached_property` **将类的方法转换为一个属性，该属性的值计算一次，然后在实例的生命周期中将其缓存作为普通属性**（一次计算多次使用）。与 property() 类似，但添加了缓存，对于在其他情况下实际不可变的高计算资源消耗的实例特征属性来说该函数非常有用。

缓存的 `cached_property()` 的机制与 `property()` 有些不同。除非定义了setter，否则常规属性会阻止属性写入。相反，缓存的 cached_property 允许写入。

缓存的 cached_property 装饰器仅在查找时运行，并且仅在同名属性不存在时运行。当它运行时，cached_property 会写入具有相同名称的属性。后续的属性读取和写入优先于缓存的 cached_property 方法，其工作方式与普通属性类似。

缓存的值可通过删除该属性来清空。 这允许 cached_property 方法再次运行。

缓存是 CPU 内部的一种高速内存，用于加速对数据和指令的访问。因此，缓存是一个可以快速访问的地方，结果可以计算并存储一次，从下一次开始，无需再次计算即可访问结果。因此，在计算费用昂贵的情况下，它非常有用。

**特定场合使用的一个属性，暂时没有用到的场合，谨慎使用。**

### partial函数

> partial 函数允许我们复刻函数的某些参数并生成新函数。函数在执行时，要带上所有必要的参数进行调用。但是，有时参数可以在函数被调用之前提前获知。这种情况下，一个函数有一个或多个参数预先就能用上，以便函数能用更少的参数进行调用。简单说就是局部套用一个函数，让广泛功能的函数简单化、单一化。这是一个 柯里化 过程。在数学和计算机科学中，柯里化是一种将使用多个参数的一个函数转换成一系列使用一个参数的函数的技术。

#### 柯里化

柯里化是一种函数的转换，它是指将一个函数从可调用的 `f(a, b, c)` 转换为可调用的 `f(a)(b)(c)`。

**柯里化不会调用函数。它只是对函数进行转换。**

```javascript
function curry(f) { // curry(f) 执行柯里化转换
  return function(a) {
    return function(b) {
      return f(a, b);
    };
  };
}

// 用法
function sum(a, b) {
  return a + b;
}

let curriedSum = curry(sum);

alert( curriedSum(1)(2) ); // 3
```

正如你所看到的，实现非常简单：只有两个包装器（wrapper）。

- `curry(func)` 的结果就是一个包装器 `function(a)`。
- 当它被像 `curriedSum(1)` 这样调用时，它的参数会被保存在词法环境中，然后返回一个新的包装器 `function(b)`。
- 然后这个包装器被以 `2` 为参数调用，并且，它将该调用传递给原始的 `sum` 函数。

**柯里化** 是一种转换，将 `f(a,b,c)` 转换为可以被以 `f(a)(b)(c)` 的形式进行调用。JavaScript 实现通常都保持该函数可以被正常调用，并且如果参数数量不足，则返回部分应用函数。柯里化让我们能够更容易地获取部分应用函数。

#### partial使用

完整语法为：`functools.partial(func, /, *args, **keywords)`，返回一个新的 partial 对象（部分对象，见下文），又称偏函数，主要用途是减少可调用对象的参数个数，当被调用时其行为类似于 func 附带位置参数 args 和关键字参数 keywords 被调用。 如果为调用提供了更多的参数，它们会被附加到 args。 如果提供了额外的关键字参数，它们会扩展并重载 keywords。 这个函数是使用 C 而不是 Python 实现的，例子如下：

```python
from functools import partial

# 常规函数
def add(a, b, c):
    return 100 * a + 10 * b + c

# b=1，c=2 的部分函数
add_part = partial(add, c = 2, b = 1)

# 调用 partial 函数
add_part(3)
# 312
```

```python
from functools import partial

def add(a,b):
    return a + b

def add2number(x,y,z):
    return x + y + z


# a 固定值为 2
add2 = partial(add,2)
add2(1)
# 3

# 将 x 固定为 1，y 值固定为 2
add3 = partial(partial(add2number,1), 2)
add3(1)
```

partial() 会被“冻结了”一部分函数参数和/或关键字的部分函数应用所使用，从而得到一个具有简化签名的新对象。

partial 对象是由 partial() 创建的可调用对象。 它们具有三个只读属性：

- partial.func：一个可调用对象或函数。 对 partial 对象的调用将被转发给 func 并附带新的参数和关键字。
- partial.args：最左边的位置参数将放置在提供给 partial 对象调用的位置参数之前。
- partial.keywords：当调用 partial 对象时将要提供的关键字参数。
