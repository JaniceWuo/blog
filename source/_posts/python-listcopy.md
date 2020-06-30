---
title: python列表复制
date: 2020-04-08 12:03:30
tags: python
---
a = [1,2,3]  b = a,则b也为[1,2,3]<br/>
这种复制方法，a和b指向同一个list，如果a改动，则b也会变，如下:
```python
a = [1,2,3]
b = a
a.append(4)
print(b)  #b=[1,2,3,4]
```
另外一种复制方法为b=a[:]，切片式复制，此时b是完全复制了一个列表。和b=list(a)效果一样。
```python
a = [1,2,3]
b = a[:]
a.append(4)
print(b)  #b=[1,2,3]
```
深复制和浅复制：（若列表中又有列表，浅复制的子列表还是会变。）
```python
import copy
a = [[1],2,3]
b = copy.copy(a)
c = copy.deepcopy(a)
a.append(4)
a[0].append(10)
print(b)  #[[1,10],2,3]
print(c)  #[[1],2,3]
```
