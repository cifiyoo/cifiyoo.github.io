---

layout: post
title: 'map&reduce'
date: 2021-08-26
categories: Python
tags: Python

---

```python
str = "www.runoob.com"
print(str.upper())          # 把所有字符中的小写字母转换成大写字母
print(str.lower())          # 把所有字符中的大写字母转换成小写字母
print(str.capitalize())     # 把第一个字母转化为大写字母，其余小写
print(str.title())          # 把每个单词的第一个字母转化为大写，其余小写 
```

`map()`函数接收两个参数，一个是函数，一个是`Iterable`，`map`将传入的函数依次作用到序列的每个元素，并把结果作为新的`Iterator`返回。即接收一个`list`会返回一个`list`。

`reduce`把一个函数作用在一个序列`[x1, x2, x3, ...]`上，这个函数必须接收两个参数，`reduce`把结果继续和序列的下一个元素做累积计算。

### 练习

利用`map()`函数，把用户输入的不规范的英文名字，变为首字母大写，其他小写的规范名字。输入：`['adam', 'LISA', 'barT']`，输出：`['Adam', 'Lisa', 'Bart']`：

```python
# -*- coding: utf-8 -*-
def normalize(name):	
    return name.capitalize()

# 测试:
L1 = ['adam', 'LISA', 'barT']
L2 = list(map(normalize, L1))
print(L2)
```

Python提供的`sum()`函数可以接受一个list并求和，请编写一个`prod()`函数，可以接受一个list并利用`reduce()`求积：

```python
# -*- coding: utf-8 -*-
from functools import reduce
def prod(L):
    return reduce(lambda x,y :x*y,L)#lambda是匿名函数，L作为参数传进lambda，以reduce的方式迭代

# 测试:
print('3 * 5 * 7 * 9 =', prod([3, 5, 7, 9]))
if prod([3, 5, 7, 9]) == 945:
    print('测试成功!')
else:
    print('测试失败!')
```

利用`map`和`reduce`编写一个`str2float`函数，把字符串`'123.456'`转换成浮点数`123.456`：

```python
# -*- coding: utf-8 -*-
from functools import reduce

def str2float(s):
	def function(x,y):
		return x*10+y
	n = s.index('.')
	s1 = list(map(int,[x for x in s[:n]]))//分割字符串
	s2 = list(map(int,[x for x in s[n+1:]]))//分割字符串
	return reduce(function,s1)+reduce(function,s2)/10**len(s2)

print('str2float(\'123.456\') =', str2float('123.456'))
if abs(str2float('123.456') - 123.456) < 0.00001:
    print('测试成功!')
else:
    print('测试失败!')
```

