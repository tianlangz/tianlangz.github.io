---
author: zty
title: Python的运算符4
date: 2022-10-01
description: Python
series:
  - Python
tags : [
    python基础
]
categories : [
    编程基础
]
series : [论文用]
aliases : [python基础]
---

运算符的使用
<!--more-->
# 算术运算符
|运算符|说明|实例|结果|
|-|-|-|-|
|+|加|12.45 + 15|27.45|
|-|减|4.56 - 0.26|4.3|
|*|乘|5 * 3.6|18.0|
|/|除|7/2|3.5|
|//|整除|7/2|3|
|%|取余|7%2|1|
|\**|幂运算/次方运算，即返回x的y次方|2**4|16|

## 加法运算
### 正常的加法运算
```python
m = 10
n = 123
sum = m + n

x = 123.456
y = 789.123
sum2 = x + y
print("sum1 = %d, sum2 = %.2f" %(sum1,sum2))
``` 
运行结果：
```
sum1=133, sum2 = 912.579
```
### 拼接字符串
<<<<<<< HEAD
当`+`用于字符串时，可以将两个字符串相拼接
=======
当`+`用于字符串时，可以将两个字符串进行拼接
```python
name = "我的博客"
url = "tianlangz.top"
c = name + "的网址："+url
print(c)
```
## 减法运算
 
>>>>>>> 926a8bd352549a9cfa559d0b7f3f55703b956ceb
