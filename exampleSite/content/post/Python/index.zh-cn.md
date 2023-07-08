---
# 帖子的发布作者
author: mimao
# 帖子的标题
title: 初识 Python
# 帖子的日期
date: 2023-07-07
# 帖子的描述
description: 初识Python并快速对其进行了解
# 帖子的标签
tags:
  - python-base
# 帖子分类
categories:
  - Python
---


# Python 基础

## python 内置模块os
```python
import os


os.listdir(path)
参数为文件夹路径，可以返回文件夹下的所有子文件夹(该子文件夹下的文件不给予返回，仅返回名称)、文件名称

os.walk(path)
参数为文件夹路径，返回3个内容：绝对路径(root)、子文件夹(dirs)、文件名(files)
此方法可以遍历文件夹下的所有文件、子文件及内的所有文件

glob.glob
glob：参数为路径以及文件过滤条件，若不设置过滤需填写为*，此函数会返回包括路径的文件夹和文件名
例如：
import glob
[print(file_abs) for file_abs in glob.glob(path)]

os.getcwd()
获取当前项目的路径

os.path.join('','',....)

os.abspath(path)

```

***

## python中列表推导式
```python
new_list = [expression(item) for item in iterable if condition]
可以写成：
new_list = []
for item in iterable:
    if condition:
        new_list.append(expression(item))

其他例子：
numbers = [2*x for x in range(1,11) if x>2 and x<5]
print(numbers)
>>> [6, 8]
```

**如果 x 的值介于2和5之间，则列表推导式返回 2*x，否则返回 3*x。**

```python
numbers = [2*x if x > 2 and x < 5 else 3*x for x in range(10)]
print(numbers)
>>> [0, 3, 6, 6, 8, 15, 18, 21, 24, 27]

numbers = []
for x in range(10):
	if x>2 and x<5:
		numbers.append(2*x)
	elif x<=2:
		numbers.append(3*x)
	else:
		numbers.append(4*x)
numbers = [2*x if x > 2 and x < 5 else 3*x if x <=2 else 4*x for x in range(10)]
print(numbers)
>>> [0, 3, 6, 6, 8, 20, 24, 28, 32, 36]


zip() 方法的使用：
cities = ['Rome', 'Warsaw', 'London']
countries = ['Italy', 'Poland', 'United Kingdom']
abc = [(city, country) for city, country in zip(cities, countries)]
print(abc)
>>> [('Rome', 'Italy'), ('Warsaw', 'Poland'), ('London', 'United Kingdom')]


嵌套列表推导式：
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
for row in matrix:
    for item in row:
        item  *= 2
print(matrix)
>>> [[2, 4, 6], [8, 10, 12], [14, 16, 18]]

变换成嵌套列表推导式
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
matrix = [[item*2 for item in row] for row in matrix]
print(matrix)
>>> [[2, 4, 6], [8, 10, 12], [14, 16, 18]]


reduce和lamba算式
from functools import reduce
numbers = [3, 6, 8, 23]
print(reduce(lambda a,b: a+b, numbers))
>>> 40
变换成列表推导式
print(sum([number for number in numbers]))
>>> 40
```
