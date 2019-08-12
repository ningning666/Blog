---
title: python 基础
abbrlink: 2
tags: 
    Python
categories:
    Python 知识汇总
---
## 数据类型和变量
### 数据类型
数据类型分为整数、浮点数、字符串、布尔值和空值
### 变量
变量可以是数字与任意数据类型

## 字符编码
字符编码使用UTF-8标准
### Python的字符串
Python的字符串支持多语言，对于单个字符的编码，Python提供了ord()函数获取字符的整数表示，chr()函数把编码转换为对应的字符
由于Python的字符串类型是str，在内存中以Unicode表示，一个字符对应若干个字节。如果要在网络上传输，或者保存到磁盘上，就需要把str变为以字节为单位的bytes。
Python对bytes类型的数据用带b前缀的单引号或双引号表示：
``` bash
x = b'ABC'
```
注意：区分'ABC'和b'ABC'，前者是str，后者虽然内容显示得和前者一样，但bytes的每个字符都只占用一个字节

以Unicode表示的str通过encode()方法可以编码为指定的bytes
英文的str可以用ASCII编码为bytes，内容是一样的，含有中文的str可以用UTF-8编码为bytes。含有中文的str无法用ASCII编码，因为中文编码的范围超过了ASCII编码的范围，Python会报错。在bytes中，无法显示为ASCII字符的字节，用\x##显示。反过来，如果我们从网络或磁盘上读取了字节流，那么读到的数据就是bytes。要把bytes变为str，就需要用decode()方法
len()函数计算的是str的字符数，如果换成bytes，len()函数计算字节数
### 格式化
运算符就是用来格式化字符串的。在字符串内部，%s表示用字符串替换，%d表示用整数替换，有几个%?占位符，后面就跟几个变量或者值，顺序要对应好。如果只有一个%?，括号可以省略。
常见的占位符有：%d（整数） %f（浮点数） %s（字符串） %x（十六进制整数） 
还有一种方式是format()方法
使用字符串的format()方法，它会用传入的参数依次替换字符串内的占位符{0}、{1}……，不过这种方式写起来比%要麻烦得多
示例如下：
``` bash
'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)
```
## list和tuple
### list
Python内置的一种数据类型是列表：list。list是一种有序的集合，可以随时添加和删除其中的元素。
示例如下：
``` bash
classmates = ['Michael', 'Bob', 'Tracy']
```
变量classmates就是一个list，list的索引是从0开始的，最后一个元素的索引是len(classmates)-1
除此之外，还可以用-1做索引,以此类推-2、-3等等
``` bash
>>>classmates[-1]
'Tracy'
```
##### list中的经常使用的方法
1.append()
list是一个可变的有序表，所以，可以往list中追加元素到末尾
``` bash
>>> classmates.append('Adm')
>>> classmates
['Michael', 'Bob', 'Tracy', 'Adm']
```
2.insert()
list可以把元素插入到指定的位置，比如索引号为1的位置
``` bash
>>> classmates.insert(1, 'Jack')
>>> classmates
['Michael', 'Jack', 'Bob', 'Tracy', 'Adm']
```
3.pop()
删除list末尾的元素
``` bash
>>> classmates.pop()
>>> classmates
['Michael', 'Jack', 'Bob', 'Tracy']
```
```bash
>>> classmates.pop(1)
>>> classmates
['Michael', 'Bob', 'Tracy']
```
pop(i)是删除指定位置的元素
4. 把某个元素替换成别的元素
``` bash
>>> classmates[1] = 'Sarah'
>>> classmates
['Michael', 'Sarah', 'Tracy']
```
5. list元素也可以是另一个list，比如：
``` bash
>>> s = ['python', 'java',['asp', 'php'], 'scheme']
>>> len(s)
4
```
### tuple

tuple是另一种有序列表即元祖，与list非常类似，但是tuple一旦初始化后就不能修改。
``` bash
>>> classmates('A', 'B', 'C')
```
现在这个classmates不能修改了，没有append，insert，pop等方法，只能正常使用classmates[0],classmates[-1],但是不能赋值成其他元素。
使得代码更安全
定义只有一个元素的tuple时必须加逗号，避免歧义
``` bash
>>> t = (1)
>>> t
1
>>> t = (1,)
>>> t
(1)
```
这是因为Python规定，这种情况下，按小括号进行计算，计算结果自然是1。
tuple里也可以定义可变的list
``` bash
>>> t = ('a', 'b', ['A', 'B'])
>>> t[2][0] = 'X'
>>> t[2][1] = 'Y'
>>> t
('a', 'b', ['X', 'Y'])
```
## 条件判断
if、 if else、 if elif else
### if语句
```bash
age = 20
if age >= 18:
    print('your age is', age)
    print('adult')
```
### if else语句
``` bash
age = 3
if age >= 18:
    print('your age is', age)
    print('adult')
else:
    print('your age is', age)
    print('teenager')
```
### if elif else语句
```bash
age = 3
if age >= 18:
    print('adult')
elif age >= 6:
    print('teenager')
else:
    print('kid')
```

##循环
Python 的循环有两种，一种是for…in循环，另一种是while循环。
### for…in循环
作用是依次把list或者tuple中的每个元素迭代出来。
```bash
names = ['Michael', 'Bob', 'Tracy']
for name in names:
    print(name)
```
输出结果如下：
```bash
Michael
Bob
Tracy
```
### while循环
只要条件满足，就不断循环，条件不满足时退出循环。比如我们要计算100以内所有奇数之和，可以用while循环实现。
```bash
um = 0
n = 99
while n > 0:
    sum = sum + n
    n = n - 2
print(sum)
```
在循环内部变量n不断自减，直到变为-1时，不再满足while条件，循环退出。
### break
break语句可以提前结束退出循环
```bash
n = 1
while n <= 100:
    if n > 10: # 当n = 11时，条件满足，执行break语句
        break # break语句会结束当前循环
    print(n)
    n = n + 1
print('END')
```
### continue
可以通过continue语句，跳过当前的这次循环，直接开始下一次循环。
```bash
n = 0
while n < 10:
    n = n + 1
    if n % 2 == 0: # 如果n是偶数，执行continue语句
        continue # continue语句会直接继续下一轮循环，后续的print()语句不会执行
    print(n)
```
## dict和set
### dict
Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。
```bash
>>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
>>> d['Michael']
95
```
注意事项：
1.一个key对应一个value，所以，多次对一个key放入value，后面的值会把前面的值冲掉
2.key不存在，dict就会报错
避免方式：一是通过in判断key是否存在
         二是通过dict的get()方法，如果key不存在，可以返回None，或者自己指定的value
3.删除key，用pop(key)方法，对应的value也会从dict中删除
### set
set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。
要创建一个set，需要提供一个list作为输入集合：
``` bash
>>> s = set([1, 2, 3])
>>> s
{1, 2, 3}
```
注意，传入的参数[1, 2, 3]是一个list，而显示的{1, 2, 3}只是告诉你这个set内部有1，2，3这3个元素，显示的顺序也不表示set是有序的。。
重复元素在set中自动被过滤：
```bash
>>> s = set([1, 1, 2, 2, 3, 3])
>>> s
{1, 2, 3}
```
##### set的增删方法
add(key): 添加元素到set中，可重复添加，但是不会有效果
remove(key): 删除元素
