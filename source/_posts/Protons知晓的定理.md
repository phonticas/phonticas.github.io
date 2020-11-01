---
title: Protons知晓的定理
author: Protons
avatar: 'https://cdn.jsdelivr.net/gh/protons-z/cdn@6.3.0/images/profile/head.jpg'
authorLink: 
authorAbout: 
authorDesc: 
categories: 文章
comments: true
date: 2020-03-04 11:20:11
tags:
keywords:
description:
photos: https://cdn.jsdelivr.net/gh/protons-z/cdn@6.3.0/images/cover1/bajbytecomputer.jpg
mathjax: true

---

本文总结出一些蒟蒻曾经遇到的定理。


## 数论

**p.s.1**下面没有特殊说明的变量一律认为是正整数

**p.s.2** 标$*$号的代表该定理结论正确但我不确定名字的定理

-------

#### 质数合数
1. 唯一分解定律(貌似小学生都会)
任意$n\in N^{+}$都满足$n=\displaystyle \prod_{i=1} p_{i}^{\alpha _{i}}$
2. 质数分布定理  
1~n中质数大约有$\frac{n}{\ln n}$
3. 约数个数定理 
$n\in N^{+}$,$n=\prod_{i=1} p_{i}^{\alpha_i}$的约数个数为$\prod_{i=1} (\alpha_{i}+1)$

-------
#### 同余问题
1. 同余定理*  
若$a\equiv b (mod\ p)$,则$a\pm c\equiv b\pm c (mod\ p)$,$a\times c\equiv b\times c(mod\ p)$
同时若$a\times c\equiv b\times c(mod\ p)$则$a\equiv b(mod\ \frac{p}{gcd(p,c)})$
1. 费马小定理 
若$p$是质数，$a^{p}\equiv a(mod\ p)$,推论当$p\nmid a$时$a^{p-1}\equiv 1(mod\ p)$
2. 欧拉定理 
若$a\bot m$,则$a^{\varphi(m)}\equiv 1(mod\ p)$

4. 中国剩余定理 
给你$n$个关于$x$同余方程,第$i$的方程为$x\equiv a_i(mod\ m_i)$ 
那么若 对于任意 $i,j$ $1\leq i$ $<$ $j\leq n$ ,$(i,j)=1$ 
则定义$M=\prod _{i=1}^{n}m_i$,$M_i=\frac{M}{m_i},t_i\equiv M_i^{-1}(mod\ m_i)$,则原方程在$mod\ M$意义下有唯一解$x \equiv \sum_{i=1}^n a_i\times t_i\times M_i(mod\ M)$

1. 扩展欧拉定理 
在 $b>\varphi(p)$ 时,$a^b\equiv a^{b\ mod \ \varphi(p)+\varphi(p)}(mod\ p)$

6. 逆元存在定理 
若$a^-1$ 在$mod\ p$意义下存在，当且仅当$(a,p)=1$
7. 某不知名定理
若$(a,p)=(b,p)=1$,$a^{x}\equiv b^{x}(mod\ p)$，且$a^{y}\equiv b^{y}(mod\ p)$ 那么$a^{(x,y)}\equiv b^{(x,y)}(mod\ p)$

------

{% emoji_coda 2233/heshui.png %}
{% emoji_coda menhera/1.jpg %}
#### 组合数问题 
1. $n>m时C^{n}_{m}=0$,$n\leq m时 C^{n}_{m}=\frac{m!}{n!\times (m-n)!}$

2. 卢卡斯定理$C^{n}_{m}\equiv C^{n\ mod\ p}_{m\ mod\ p}*C^{n/p}_{m/p}(mod\ p)$
3. $C^{n}_{m}=C^{n-1}_{m-1}+C^{n-1}_{m}$
4. $n\times C^{n}_{m}=m\times C^{n-1}_{m-1}$
5. 二项式定理 
$(1+x)^n=\displaystyle \sum ^{n}_{k=0} C_{n}^{k}\times x^k$
##### Update 2020.3.7(NOI Online) $Update$
每次冒泡排序，对于任意第i位，$C_{i}$为第i位的逆序数个数，$C_{i}=max(C_{i}-1,0)$

这个坑太大了，我不想填了，考试中遇到好玩的也会咕咕咕的呀
