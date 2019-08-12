---
abbrlink: '3'
title: 'python 基本函数'
tags: 
    Python
categories:
    Python 知识汇总
---
## 基本函数语法
### 定义函数
在Python中，定义一个函数要使用def语句，依次写出函数名、括号、括号中的参数和冒号:，然后，在缩进块中编写函数体，函数的返回值用return语句返回。
我们以自定义一个求绝对值的my_abs函数为例：
``` bash
def my_abs(x):
    if x >= 0:
        return x
    else:
        return -x
```
### 调用函数
```bash
>>> print(my_abs(-99))
99
```
### 空函数
定义一个什么也不做的空函数
``` bash
def nop():
    pass   #pass可以用来作为占位符，比如现在还没想好怎么写函数的代码，就可以先放一个pass，让代码能运行起来
```
### 参数检查
参数个数检查，python解释器会自动检查出来，并抛出TypeError
参数类型检查，使用isinstance()
``` bash
def my_abs(x):
    if not isinstance(x, (int, float)):
        raise TypeError('bad operand type')
    if x >= 0:
        return x
    else:
        return -x
```
若输入参数出现错误，会抛出一个错误
## 函数的参数
### 位置参数
``` bash
def power(x):
    return x * x
>>> power(5)
>>> 25
```
``` bash
def power(x, n):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
>>> power(5,3)
125
```
根据定义的参数个数传入几个位置参数
### 默认参数
设置的默认参数也可以在函数调用时明确传入，更改默认参数
``` bash
def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
>>>  power(5)
25
>>> power(5, 3)
125
```
注意：默认参数必须指向不变对象

### 可变参数
当参数个数不确定时，我们可以把这些不确定的参数当作一个list或者tuple传递进来
例如：以数学题为例，给定一组a,b,c,……，计算他们的平方和
```bash
def calc(numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
>>> calc([1, 2, 3])
14
>>> calc((1, 3, 5, 7))
84
```
这种方式需要先组装出一个list或者tuple
但是利用可变参数，调用函数的方式可以简化成这样：
```bash
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
>>> calc(1, 2)
5
>>> calc()
0
```
定义可变参数和定义一个list或tuple参数相比，仅仅在参数前面加了一个 * 号。在函数内部，参数numbers接收到的是一个tuple，因此，函数代码完全不变。但是，调用该函数时，可以传入任意个参数，包括0个参数
如果已经有一个list或者tuple，要调用一个可变参数,Python允许你在list或tuple前面加一个*号，把list或tuple的元素变成可变参数传进去
```bash
>>> nums = [1, 2, 3]
>>> calc(*nums)
14
```
### 关键字参数
可变参数传入0个或者任意多个参数，在调用时自动组装为一个tuple，关键字参数传入0个或者多个含参数名的参数，这些关键字参数在函数内部自动组装成一个dict
示例如下：
``` bash
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
>>> person('Bob', 35, city='Beijing')
name: Bob age: 35 other: {'city': 'Beijing'}
>>> person('Adam', 45, gender='M', job='Engineer')
name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
```
关键字参数有什么用？
它可以扩展函数的功能。比如，在person函数里，我们保证能接收到name和age这两个参数，但是，如果调用者愿意提供更多的参数，我们也能收到。试想你正在做一个用户注册的功能，除了用户名和年龄是必填项外，其他都是可选项，利用关键字参数来定义这个函数就能满足注册的需求。
### 命名关键字参数
如果要限制关键字参数的名字，可以用命名关键字参数
示例如下：
```bash
def person(name, age, *, city, job):
    print(name, age, city, job)
>>> person('Jack', 24, city='Beijing', job='Engineer')
Jack 24 Beijing Engineer
```
和关键字参数**kw不同，命名关键字参数需要一个特殊分隔符*，*后面的参数被视为命名关键字参数
但是如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符*了
命名关键字参数必须传入参数名，这和位置参数不同。如果没有传入参数名，调用将报错
```bash
def person(name, age, *args, city, job):
    print(name, age, args, city, job)
>> person('Jack', 24, 'Beijing', 'Engineer')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: person() takes 2 positional arguments but 4 were given
```
### 参数组合
在Python中定义函数，可以用必选参数、默认参数、可变参数、关键字参数和命名关键字参数，这5种参数都可以组合使用。但是请注意，参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数
** 关键字参数与命名关键字参数对应的是字典dict，可变参数对应的是元组