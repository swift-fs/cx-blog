---
title: "Python专题 | Python入门"
description: ""
pubDatetime: 2023-07-11T18:00:00+08
postSlug: python-start
featured: true
draft: false
tags:
  - python
  - python专题
---

### 基本格式

- Python 使用缩进来组织代码块，而不是{}
- Python 是区分大小写的

### 注释

#### 单行注释

```pytho
#单行注释
```

#### 多行注释

```python
'''多行注释01'''
"""多行注释02"""
```

### 海龟画图

不懂没事，编程兴趣轻松拿捏。

```python
import turtle

turtle.showturtle()
turtle.write("你好")
turtle.forward(300)  # 向前300px
turtle.color('red')
turtle.left(90)
turtle.forward(300)
turtle.goto(0, 50)  # 前往指定坐标
turtle.goto(0, 0)
turtle.penup()  # 抬起画笔
turtle.goto(0, 300)
turtle.pendown()  # 放下画笔
turtle.circle(100)
turtle.done()
```

奥运五环：

```python
import turtle

# turtle.showturtle()

turtle.width(10)
turtle.color("blue")
turtle.circle(50)

turtle.penup()
turtle.color("black")
turtle.goto(80, 0)
turtle.pendown()
turtle.circle(50)

turtle.penup()
turtle.color("red")
turtle.goto(160, 0)
turtle.pendown()
turtle.circle(50)

turtle.penup()
turtle.color("yellow")
turtle.goto(40, -50)
turtle.pendown()
turtle.circle(50)

turtle.penup()
turtle.color("green")
turtle.goto(110, -50)
turtle.pendown()
turtle.circle(50)

turtle.done() # 程序一直保持运行
```

### Python 程序的构成

- 每个.py 文件就是一个模块，python 程序由各个模块组成
- 语句是模块内的基本单元
- python 强制使用缩进来组织代码块
- 一行代码较长，可以使用使用`\`行连接符换行

### 一切皆对象

- Python 中，一切皆对象
- 每个对象由：标识（id），类型（type），值（value）组成

> 标识唯一标识对象，通常对应计算机中的内存地址，也叫指针，使用内置函数 id(obj)可以获取对象的标识
>
> 类型用于表示对象的存储类型，可以使用内置函数 type(obj)获取对象的类型
>
> 值表示对象存储的具体数据，可以通过 print(obj)直接打印出值

> 对象的本质：一个内存块，拥有特定的值，支持特定类型的相关操作。

```python
a = 3
print(a)
print(type(a))
print(id(a))
b = "我爱你"
print(b)
print(type(b))
print(id(b))
```

#### 引用

在 Python 中，变量也称为引用（reference）。变量存储的是对象的地址。变量通过地址指向（引用）了对象。 变量位于栈内存，对象位于堆内存。Python 是动态类型，所以不用显式指定变量类型，因为变量可以通过引用的对象确定类型。

### 标识符

用来起名的规则，名包括：函数名，变量名，类名等，规则如下：

- 前缀必须是：字母，下划线
- 后续可以包括：字母，数字，下划线
- 不能包括关键字
- 尽量避免使用`__xxx__`这种格式

### 变量

变量使用前，要先进行声明和赋值。对象如果没有被任何对象引用，会被垃圾回收机制进行回收，清空所占用的内存空间。可以使用`del xxx`来删除不需要再使用的变量。

```python
a = 10
print(a)
del a
print(a) # 报错，因为已经被垃圾回收
```

### 常量

```python
# 逻辑常量，仍然可以修改
MAX_AGE = 150
print(MAX_AGE)
MAX_AGE = 200
print(MAX_AGE)

# 链式赋值
x = y = 200
print(x)
print(y)

# 系列解包
a, b, c = 100, 200, 300
print(a, b, c)

# 互换a,b的值
a, b = b, a
print(a)
print(b)
```

常量一般使用大写，多个单词使用下划线隔开。

### 四种基本内置类型

```python
a = 123
b = 3.14
c = True
d = "hello,world"

print(type(a))  # <class 'int'>
print(type(b))  # <class 'float'>
print(type(c))  # <class 'bool'>
print(type(d))  # <class 'str'>

a1 = 10 / 5  # 浮点数除法
print(a1)  # 2.0
a2 = 10 // 5  # 整数除法
print(a2)  # 2
```

#### 整数

```python
a = 0b1011  # 二进制
b = 0o17  # 八进制
c = 0x1f  # 十六进制
print(a)  # 11
print(b)  # 15
print(c)  # 31

# 强制转换为整型，浮点数会舍弃小数点后，字符串需要能转换为整型才可以
d = 9.8
d1 = "123"
f = int(d)  # 9
f1 = int(d1)  # 123

# python中，整型不会溢出，可以无穷大
e = 10 ** 1000
print(e)
```

#### 浮点数

```python
a = 3.14
b = 10

# 整数和浮点数运算，结果为浮点数
c = a + b
print(c)

d = 3.14
# 四舍五入 返回整数
f = round(d)
print(f)
print(type(f))

e = "12.45"
# 转换为浮点数
print(float(e))
```

#### 小例子

```python
import turtle

x1, y1 = 100, 100
x2, y2 = 100, -100
x3, y3 = -100, -100
x4, y4 = -100, 100

turtle.penup()
turtle.goto(x1, y1)
turtle.pendown()
turtle.goto(x2, y2)
turtle.goto(x3, y3)
turtle.goto(x4, y4)
turtle.write(f'{x1 - x4},{y1 - y4}')
turtle.done()
```

### 运算符

```python
# 非零即为真
a = True
b = 5
print(a + b)  # 6
print(bool(b))

# 逻辑运算符
d = True
f = False
print(d and f)  # False 与
print(d or f)  # True 或
print(not d)  # False 非

e = 90
# 连续关系运算符在python中是支持的，但是不建议
h = 100 < e < 200
print(h)

# 字符串
str1 = "hello"
str2 = "world"
# 字符串拼接
str3 = str1 + str2
```

### is || eq

```python
# is比较变量是否为同一个对象，是否指向同一个内存地址
# 判断变量是否为None时，使用is效率更高
# == 比较连个变量的值是否相等，默认调用对象的__eq__方法

# 整数会被缓存
a = 30
b = 30
print(a is b)  # True

# 字符串也会被缓存
str1 = "hello"
str2 = "hello"
print(str1 is str2)  # True

# 判断字符串是否包含某一部分
print("abc" in "abcd")
```

### 字符串

#### 基本操作

```python
# 字符串的本质是字符序列
# python不支持单字符类型，单字符也是作为一个字符串使用
# python使用的Unicode字符集


name = "汤姆"
# 获取字符串长度
print(len(name))
# 转义字符,使用\+特殊字符
print("哈哈\n，嘿嘿")

desc = "是一只猫"
age = 10

# 字符串拼接
print(name + desc)
print(name + str(age) + desc)

str01 = "哈哈，你是猪"
# 重复10次
print(str01 * 10)

# 控制台输入，返回的都是字符串
input01 = input("请输入名称：")
input02 = input("请输入年龄：")
print(input01)
print(int(input02))
```

#### 常用操作

```python
a = "google kiss oh my god"

# 替换
b = a.replace('g', 'h', )
print(b)
# 提取
a1 = a[:5:2]
print(a1)
print(a)

# 分割
s = "i am tom"
l = s.split()
print(l)
print(type(l))

# 连接
s1 = " ".join(l)
print(s1)

s2 = "大河之水天上来，前三散尽还福来大河，8527，Kiss"

# 字符串长度
print(len(s2))
# 是否以指定字符串开头
print(s2.startswith("大河"))
# 是否以指定字符串结尾
print(s2.endswith("27"))
# 第一次出现指定字符串的位置
print(s2.find("来"))
# 最后一次出现指定字符串的位置
print(s2.rfind("来"))
# 指定字符串出现的次数
print(s2.count("大河"))
# 所有字符串是否全是字母和数字
print(s2.isalnum())
# 去除首位的指定字符串
print(s2.strip("大河"))
# 全部大写
print(s2.upper())
# 全部小写
print(s2.lower())
a = "TXT"
# 字符串填充指定长度
print(a.center(12, "*"))
```

#### 可变字符串

```python
import io

s = "11 kiss"
sio = io.StringIO(s)  # 可变字符串
print(sio)
print(sio.getvalue())
# 指针移动到字符串自定的索引位置
sio.seek(3)
# 在指针停留的位置写入字符串
sio.write("哈哈")
print(sio.getvalue())
```

### 序列

> 序列天天见。

序列是一种数据存储方式，用来存储一系列的数据。在内存中，数据是一块用来存放多个值的连续的内存空间。

#### 列表创建

```python
# 字符串转列表
l1 = list("kiss cp")
print(l1)
# 普通方法创建列表
l2 = ["kiss", "cp"]
print(l2)

# rang生成列表
l3 = list(range(0, 10, 1))
print(l3)

# 推导式
l4 = [x * 3 for x in range(0, 10)]
print(l4)
```

#### 列表元素的添加

```python
l1 = [1, 2, 5, 8, 0]
# 01
l1.append(18)
print(l1)
# 02
l1.extend([10, 20])
print(l1)

# 03
l1 = l1 * 2
print(l1)
# 04
l1 = l1 + [9, 1]
print(l1)

# 05
l1.insert(1, 1908)
print(l1)
```

#### 列表元素删除

删除的本质同样是元素的拷贝，因为要保持内存块连续。

```python
l1 = [1, 2, 6, 9, 0, 2]
# 01
# del l1[-1]
# print(l1)

# 02
# l1.pop()
# print(l1)

# 03
# l1.remove(2)
# print(l1)
```

#### 列表元素访问

```python
list01 = [1, 3, 5, 7, 9, 1]
# 元素出现次数
print(list01.count(1))
# 元素第一次出现的索引
print(list01.index(3))
# 通过索引访问元素
print(list01[4])
# 列表长度
print(len(list01))
# 元素是否在列表中
print(2 in list01)
print(3 in list01)
print(100 not in list01)
```

#### 列表切片

```python
list02 = [1, 2, 5, 8, 0]

# 列表切片
list03 = list02[:2]
print(list03)

# 复制一个列表
list04 = list02[:]
print(list04)

# 列表切片，每隔3个取一个
list05 = list02[::3]
print(list05)
```

#### 列表复制/排序/遍历/最大*最小*和

```python
import random

a = [10, 5, 20, 60, 30]
print(a)
# 原列表排序
a.sort()
print(a)
a.sort(reverse=True)

print(a)

# 随机排序
random.shuffle(a)

b = [1, 2, 5, 8, 0]
# 列表复制
b1 = [] + b
print(b)
print(id(b))
print(id(b1))

c = [11, 9, 670, 33]
# 排序，产生新的列表
c1 = sorted(c)
print(c)
print(c1)

# 遍历
for obj in c:
    print(obj)

a = [10, 90, 100, 3]

print(max(a))
print(min(a))
print(sum(a))
```

#### 多维列表

实际工作中，最多用到二维数组，一维的代表线性数据，二维的可以代表表格数据，如工作中常用的 excel 表格就可以使用二维数组进行表达。

```python
table = [
    ["小微", 19, 19800],
    ["小王", 20, 32000],
    ["小孙", 32, 36000]
]

for item in table:
    # print(item)
    for inner in item:
        print(inner, end="\t")
    print("\n")

print(table[0][0])
rint("\n")
```

#### 元组定义

```python
# 元组是不可变的列表，没有增删改的方法
t1 = (1, 2, 5, 8, 0)
print(t1)
print(type(t1))

t2 = 1, 2, 5, 8, 0
print(t2)
print(type(t2))

t3 = (1,)
print(t3)
print(type(t3))

# 整型int
i4 = (1)
print(i4)
print(type(i4))

# tuple(x)，可以接受列表，字符串，其他序列类型，迭代器生成元组
# list(x)，可以接受元组，字符串，其他序列类型，迭代器生成列表

l1 = [1, 2, 5, 8]
# 列表转元组
t4 = tuple(l1)
print(t4)
print(type(t4))

# 元组转列表
l2 = list(t4)
print(l2)
print(type(l2))
```

#### 元组其他

```python
# 列表推导式
a = [x * 10 for x in range(1, 10)]
print(a)

# 生成器
b = (x * 2 for x in range(1, 20))
print(b)
t = tuple(b)
print(t)

b1 = (x * 2 for x in range(3))
# 通过__next__方法访问生成器的元素
print(b1.__next__())
print(b1.__next__())

c = ["小红"]
d = [17, 19, 12]
f = [3247, 1896, 5678]
# 多列表聚合
r = zip(c, d, f)

# l01 = list(r)
# print(l01)

t01 = tuple(r)
print(t01)
```

#### 字典的创建方式

```python
# 最常用
d1 = {
    "name": "小吴",
    "age": 18,
    "gender": True
}

print(d1)
print(type(d1))

# 常用
d2 = dict(name="小红", age=20, gender=False)
print(d2)
print(type(d2))

# 较常用
d3 = dict([("name", "小绿"), ("age", 90)])
print(d3)
print(type(d3))

# 较常用
keys = ["name", "age", "gender"]
values = ["天下", 29, False]
d4 = dict(zip(keys, values))
print(d4)
print(type(d4))

# 非常少用
d5 = dict.fromkeys(keys, )
print(d5)
print(type(d5))

# 字典的key必须是不可变对象，元组可以当做key，但是列表不行
```

#### 字典常用操作

```python
d1 = {
    "name": "小王八",
    "age": 6986,
    "gender": True
}

print(d1["name"])

# 最常用
print(d1.get("name"))

# 不存在key会报错
# print(d1["age01"])

# 不存在的key，可以指定获取不到的 默认值
print(d1.get("age01", 18))
print(list(d1.items()))
print(list(d1.keys()))
for key in d1.keys():
    print("key:", key)
print(d1.values())
# 字典中键值对数量
print(len(d1))
# key是否在字典中
print("age01" in d1)
```

```python
d1 = {
    "name": "小王八",
    "age": 6986,
    "gender": True
}
# d1.setdefault("address")
# 增加
d1["hobbies"] = ["吃饭"]
print(d1)
d1.setdefault("height", 180)
print(d1)

# 删除指定键值对
del d1["hobbies"]
print(d1)
# 删除所有键值对
d1.clear()

# 修改
d1["height"] = 160
print(d1)
```

```python

```

### 推导式

#### 列表推导式

```python
[表达式 for item in 可迭代对象]
```

#### 字典推导式

```python
{健：值 for item in 可迭代对象}
```

#### 集合推导式

```python
{表达式 for item in 可迭代对象}
```

#### 生成器推导式

没有元组推导式，生成器推导式可以转换成其他的数据结构，一个生成器只能运行一次。

```python
(表达式 for item in 可迭代对象)
```

#### 综合使用

绘制同心圆：

```python
import turtle

circles = [
    ('red', 10),
    ('green', 20),
    ('blue', 30),
    ('orange', 40)
]

for color, radius in circles:
    turtle.penup()
    turtle.setx(0)
    turtle.sety(-radius)
    turtle.pensize(2)
    turtle.pendown()
    turtle.color(color)
    turtle.circle(radius, )

turtle.done()

```

### 函数

函数是可重用的代码块，主要解决代码复用性。每个函数代表一个任务或者功能。

```python
# 函数定义
def print_max(a: int, b: int) -> int:
    """
    文档字符串
    返回两个数中的较大值
    :param a: 参数1
    :param b: 参数2
    :return: 返回较大的值
    """
    if a > b:
        return a
    return b


# 函数调用
print(print_max(100, 20))

# 可以通过help获取文档字符串
help(print_max)

```

#### 返回值

通过return返回值，两个主要作用：

- 结束函数执行
- 返回一个值给调用者

如果函数不包含return，默认函数执行完毕后返回None

#### 函数也是对象

Python中一切都是对象。

```python
def print_star(n: int):
    print("*" * n)


print(print_star)
print(type(print_star))
print(id(print_star))

c = print_star
c(10)

d = print_star
d(20)
print(d)
print(type(d))
print(id(d))

```

#### 变量作用域

全局变量：函数和类外边声明的变量。作用域为所定义的模块，从定义位置开始，直到模块结束。

局部变量：在函数体内声明的变量。

函数体内，局部变量的优先级高于全局变量。局部变量的执行效率更高。

```python
global_a = 100


def func1():
    # 函数内修改全局变量，使用global关键字进行声明
    global global_a
    b = 3
    print(global_a)
    print(b)
    global_a = 109


func1()
print(global_a)  # 109

```

#### 参数的传递

Python中的赋值都是引用传递，包括函数调用实参往形参传值。

```python
l1 = [10, 20, 30]


def fun1(m: list):
    m.append(100)
    print("m:", id(m))


fun1(l1)
print("l1:", id(l1))
print(l1)

```

#### 深浅拷贝

```python
l1 = [10, 20, [30, 40]]

import copy

# 浅拷贝
l2 = copy.copy(l1)
# 深拷贝
l3 = copy.deepcopy(l1)
l1[0] = 11

print(l1)
print(l2)
print(l3)

l1[2][0] = 99
print(l1)
print(l2)
print(l3)

```

#### 参数类型

```python
# a,b位置参数
# c默认参数
def func1(a, b, c=10):
    print(a, b, c)


func1(10, 20)
func1(10, 20, 30)
# 命名参数
func1(c=200, a=9, b=6)

```

```python
# *args 可变参数
# **kwargs 可变命名参数
def func(a, b, c, *args, **kwargs):
    print(a, b, c)
    print(args)
    print(kwargs)


func(10, 20, 30, 100)
func(10, 20, 30, 100, name="哈哈", age=10, gender=True)

```

#### lambda

一般不推荐使用

```python
f = lambda a, b, c: a + b + c
print(f(10, 20, 30))

```

#### eval()

一般不推荐使用

功能：将字符串当成有效的语句来执行并返回结果。

```python
str1 = "print('hello world')"
eval(str1)

dict1 = dict(c=100861, a=10)
str2 = '''
a+c
'''
d = eval(str2, dict1)
print(d)

```

#### 嵌套函数

```python
# 嵌套函数
def outer():
    print("outer func")
    b = 10086

    def inner():
        nonlocal b  # 声明外部函数的局部变量
        print("inner func")
        print(b)
        b = 109

    inner()
    print(b)


outer()

```

#### LEGB规则

python在查找变量时，按照LEGB规则（局部，外部函数，全局，内置）。









