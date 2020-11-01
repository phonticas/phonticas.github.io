---
title: python3一些常用操作
author: Protons
avatar: 'https://cdn.jsdelivr.net/gh/protons-z/cdn@6.3.0/images/profile/head.jpg'
authorLink: 
authorAbout: 
authorDesc: 
categories: 笔记
comments: true
date: 2020-08-23 21:59:11
tags: 
- python3
keywords:
description:
photos: https://cdn.jsdelivr.net/gh/protons-z/cdn@6.1.6/images/cover/23.jpg
mathjax: true
---

我用的是python3.8.1
本文大概记录一下python最基础的（和OI）有关的一些操作。
## 最重要的！！！
python不同于c++/Java 
python通过缩进来确定代码的逻辑
不同于c++/c/Java使用`{` `}`来确定代码逻辑
所以想表达类似
``` cpp
if(opt){
    puts("xxxx");
}
```
在python中要
``` python
if opt :
    print(xxxxx)
```
同时python是支持交互形式的
所以要是想像写c++这么写建议装一个vscode或者其他支持python的编译器以获最佳体验

---

### python 读入字符串

``` python
s=input()
```
### python字符串转整形
``` python
s=input()
print(int(s))
```

### python for循环
``` python
for i in range(n):
    print(i)
#从0到n-1
for i in range(l,r):
    print(i)
#从l到r-1
for i in range(a,b,c):
    print(i)
#从a到b-1步长是c
```

### python 函数
``` python
def oxo(a,b,c):
    print(a+b+c)
```

### python 数组（字典）
``` python
dic={}
dic['sss']='esdp'
dic[1]='esd'
dic[-1]=333
print(dic[1])
print(dic[-1])
print(dic['sss'])
```

### python 数组（列表）
``` python
g=[]
#列表下标从0开始
g.append(1)
#再列表最后插入1类似c++的push_back
g.append('ssss')
g.append('qbs')
g.append('msannu')
g[1]='-wes'
#修改'1'的位置的值
del g[1]
#删除'1'这个位置
print(g)
```

### python 文件写入
``` python
#新建s.in并且写入
file=open('s.in','w')
file.write('xywcjwyy')
``` 
### python 文件读入
``` python
#读入s.in文件全部读完
file=open('s.in')
print(file.read())
```

### python 随机数
``` python
import random
for i in range(10):
    print(random.uniform(1,20))
#随机浮点
for i in range(10):
    print(random.randint(1,20))
#随机整型
g=[1,3,2,4,2,1]
random.shuffle(g)
print(g)
#random shuffle随机排序

l=[1,'ss','sdd','dd',-1,1e9]
pec=random.choice(l)
print(pec)
#有限集合内随机选取
```