---
title: "Python专题 | Python入门"
description: ""
pubDatetime: 2023-07-11T18:00:00+08
postSlug: python-async
featured: false
draft: false
tags:
  - python
  - python专题
---

### 基本格式

- Python使用缩进来组织代码块，而不是{}
- Python是区分大小写的

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

### Python程序的构成

- 每个.py文件就是一个模块，python程序由各个模块组成
- 语句是模块内的基本单元
- python强制使用缩进来组织代码块
- 一行代码较长，可以使用使用`\`行连接符换行

### 一切皆对象

- Python中，一切皆对象
- 每个对象由：标识（id），类型（type），值（value）组成

> 标识唯一标识对象，通常对应计算机中的内存地址，也叫指针，使用内置函数id(obj)可以获取对象的标识
>
> 类型用于表示对象的存储类型，可以使用内置函数type(obj)获取对象的类型
>
> 值表示对象存储的具体数据，可以通过print(obj)直接打印出值

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

在Python中，变量也称为引用（reference）。变量存储的是对象的地址。变量通过地址指向（引用）了对象。 变量位于栈内存，对象位于堆内存。Python是动态类型，所以不用显式指定变量类型，因为变量可以通过引用的对象确定类型。

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



