---
abbrlink: '5'
title: '高级特性'
tags: 
    Python
categories:
    Python 知识汇总
---
## 切片

取一个list或tuple的部分元素是非常常见的操作，例如，一个lst如下：

``` bash
L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
```

用切片可以选择任意位置取元素

``` bash
L[0:3]  #取前三个元素
L[:]   #全部复制
L[-2:] #从倒数第二个向后取
```

输出结果如下所示：

``` bash
['Michael', 'Sarah', 'Tracy']
['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
['Bob', 'Jack']]
```

同理字符串也可以这样操作

## 迭代

Python的for循环抽象程度要高于C的for循环，因为Python的for循环不仅可以用在list或tuple上，还可以用在其他可迭代对象上。
举例：dict迭代

``` bash
d = {'a': 1, 'b': 2, 'c': 3}
for key in d:
    print(key)
```

输出结果为：

``` bash
a
c
b
```

**因为dict的存储不是按照list的方式顺序排列，所以，迭代出的结果顺序很可能不一样。**
**默认情况下，dict迭代的是key。如果要迭代value，可以用for value in d.values()，如果要同时迭代key和value，
可以用for k, v in d.items()。**
当我们使用for循环时，只要作用于一个可迭代对象，for循环就可以正常运行，而我们不太关心该对象究竟是list还是其他数据类型。
那么，如何判断一个对象是可迭代对象呢？方法是通过collections模块的Iterable类型判断：

``` bash
>>> from collection import Iterable
>>> isinstance('abc',Iterable)  #是否可迭代
>>> True
```

若对list实现类似Java那样的下标循环，可以使用Python内置的enumerate函数可以把一个list变成索引-元素对

```bash
>>> for i, value in enumerate(['A', 'B', 'C']):
>>>     print(i, value)
0 A
1 B
2 C
```

请使用迭代查找一个list中最小和最大值，并返回一个tuple：
自己写的示例代码

``` bash
def findMinAndMax(L):
if L==[]:
        return(None,None)
    else:
        min=max=L[0]
        for i in L:
            if i<min:
                min=i
            if i>max:
                max=i
        return(min,max)
```

## 列表生成式

列表生成式即List Comprehensions，是Python内置的非常简单却强大的可以用来创建list的生成式。
举个例子，要生成list [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]可以用list(range(1, 11))：

``` bash
>>> list(range(1, 11))
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

但如果要生成[1x1, 2x2, 3x3, ..., 10x10]怎么做？方法一是循环：

``` bash
>>> L = []
>>> for x in range(1, 11):
...    L.append(x * x)
...
>>> L
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

但是循环太繁琐，而列表生成式则可以用一行语句代替循环生成上面的list：

```bash
>>> [x*x for x in range(1,11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

for循环后面还可以加上if判断，这样我们就可以筛选出仅偶数的平方：

``` bash
>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]
```

还可以使用两层循环，可以生成全排列：

``` bash
>>> [m + n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
```

for循环其实可以同时使用两个甚至多个变量，比如dict的items()可以同时迭代key和value,列表生成式也可以使用两个变量来生成list：

```bash
>> d = {'x': 'A', 'y': 'B', 'z': 'C' }
>>> [k + '=' + v for k, v in d.items()]
```

输出结果如下：

``` bash
['y=B', 'x=A', 'z=C']
```

练习题： L1为 ['Hello', 'World', 18, 'Apple', None]，输出 L2为 ['hello', 'world', 'apple']
代码如下：

``` bash
L2 = [i.lower() for i in L1 if isinstance(i, str)==True]
```

## 生成器

通过列表生成式，我们可以直接创建一个列表。但是，受到内存限制，列表容量肯定是有限的。而且，创建一个包含100万个元素的列表，不仅占用很大的存储空间，如果我们仅仅需要访问前面几个元素，那后面绝大多数元素占用的空间都白白浪费了。
所以，如果列表元素可以按照某种算法推算出来，那我们是否可以在循环的过程中不断推算出后续的元素呢？这样就不必创建完整的list，从而节省大量的空间。在Python中，这种一边循环一边计算的机制，称为生成器：generator。
要创建一个generator，有很多种方法。第一种方法很简单，只要把一个列表生成式的[]改成()，就创建了一个generator：

``` bash
>> L = [x * x for x in range(10)]
>>> L
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
>>> g = (x * x for x in range(10))
>>> g
<generator object <genexpr> at 0x1022ef630>
```

创建L和g的区别仅在于最外层的[]和()，L是一个list，而g是一个generator。如果要一个一个打印出来，可以通过next()函数获得generator的下一个返回值：

``` bash
>>> next(g)
0
>>> next(g)
1
```

generator保存的是算法，每次调用next(g)，就计算出g的下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出StopIteration的错误
不想一个一个打印也可以用for循环进行打印

``` bash
>>> g = (x * x for x in range(10))
>>> for n in g:
...     print(n)

0
1
4
9
16
25
36
49
64
81
```

第二种创建generator的办法是使用yield关键字
generator和函数的执行流程不一样。函数是顺序执行，遇到return语句或者最后一行函数语句就返回。而变成generator的函数，
在每次调用next()的时候执行，遇到yield语句返回，再次执行时从上次返回的yield语句处继续执行。
练习题：杨辉三角

``` bash
                1
            1       1
        1       2       1
    1       3       3       1
1       4       6       4       1
```

把每一行看做一个list，试写一个generator，不断输出下一行的list：

``` bash
def triangles():
    a=[1]
    while True:
        yield a
        a=[sum(i) for i in zip([0]+a,a+[0])]
n=0
for t in triangles():
    print(t)
    n=n+1
    if n == 10:
        break
```

## 迭代器

凡是可作用于for循环的对象都是Iterable类型；
凡是可作用于next()函数的对象都是Iterator类型，它们表示一个惰性计算的序列；
集合数据类型如list、dict、str等是Iterable但不是Iterator，不过可以通过iter()函数获得一个Iterator对象。
Python的for循环本质上就是通过不断调用next()函数实现的，例如：

``` bash
for x in [1, 2, 3, 4, 5]:
    pass
```

实际上完全等价于：

``` bash
# 首先获得Iterator对象:
it = iter([1, 2, 3, 4, 5])
# 循环:
while True:
    try:
        # 获得下一个值:
        x = next(it)
    except StopIteration:
        # 遇到StopIteration就退出循环
        break
```
