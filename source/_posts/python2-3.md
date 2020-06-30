---
title: python2和python3在除法上的区别
date: 2020-03-24 20:47:05
categories: python
---
几年前装上python3之后就没用过python2了，但是刚刚在牛客网刷题时，编辑器只有python2没有python3，于是遇到坑了。我检查一遍代码觉得没有错，又复制到本地sublime上运行一遍也没问题，但是在牛客网上只通过16%的样例。
想了一下可能是python版本问题，最后找到原因。在python2中：
```python
3/2=1
```
在python3中：
```python
3/2=1.5
```
这导致的后果是在执行代码`while small<sum/2`时，若small=1，sum=3，在python2中会认为不满足条件，导致程序返回结果出错，而在python3中代码是对的。

