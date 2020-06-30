---
title: 【编程题】bit 位数
date: 2020-03-28 20:48:16
categories: 算法
---
## 题目描述
两个int32整数m和n的二进制表达，计算有多少个位(bit)不同？
例如输入15,8 输出3
因为15 = 1111  8 = 1000  有3位不同

代码:
```Python
import sys
def main():
	line = sys.stdin.readline()
	a,b = map(int,line.split())
	a = bin(a).replace("0b","")
	b = bin(b).replace("0b","")
	n = max(len(a),len(b))
	a = a.rjust(n,'0')
	b = b.rjust(n,'0')
	count = 0
	for i in range(n):
		if a[i]!=b[i]:
			count+=1
	print(count)

if __name__ == '__main__':
	main()
```
知识点：python中的`bin()`可以直接将int型转换为2进制，输出格式为0b****，所以这里要把0b去掉。
而且转换后位数不同，这里取最长的位数，用`rjust()`向右对齐，左边空缺处补0。