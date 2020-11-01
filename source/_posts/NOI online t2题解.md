---
title: NOI online t2题解
author: Protons
avatar: 'https://cdn.jsdelivr.net/gh/protons-z/cdn@6.3.0/images/profile/head.jpg'
authorLink: 
authorAbout: 
authorDesc: 
categories: 题解
comments: true
date: 2020-03-05 11:20:11
tags:
keywords:
description:
photos: https://cdn.jsdelivr.net/gh/protons-z/cdn@6.3.0/images/cover/7.jpg
mathjax: true

---
##### Noi online t2 爆零记{% emoji_coda 2233/yumen.png %}

##### [题目链接](https://www.luogu.com.cn/problem/P6186)


记$a_i$为原数组
首先我们要知道一个性质
就是记$c_{a_i}$ 为在第$i$位前且比第$i$大的数的个数
每一次冒泡后,$c_{a_i}=max(c_{a_i-1},0)$ 
为什么？~~可以手玩试试~~ 
看看题目给的伪代码 
``` cpp
for i = 1 to n-1:
  if p[i] > p[i + 1]:
    swap(p[i], p[i + 1])
```
我们都知道冒泡排序每次是在将未排好序的数中最大数向后冒
观察若对于第$i$位,$a_i>a_{i+1}$则一次冒泡后变为$a_{i+1},...$
则$a_{i+1}$后面所有没排好序的数$a_k$其$c_{a_k}$都会$-1$
当然$c_{a_k}=0$时就不管他了 
那我们的工作就是维护$c$这个数组 
更改直接分类讨论 
那求值就为$\displaystyle \sum_{i=1}^{n}max(0,c_{a_i}-k)$ 
所以因为答案为零的是不会有贡献的所以我们化为 
$\displaystyle \sum _{c_{a_i}>k} c_{a_i}-k$ $=$ $\displaystyle \sum _{c_{a_i}>k} c_{a_i}-\displaystyle \sum _{c_{a_i}>k}k$ 
然后就是树状数组的模板了 
$tips1:$ 注意k的大小,若k>n就一定排好序了 
$tips1:$ 注意是树状数组,下标不为零 
``` cpp
#include<bits/stdc++.h>
#ifdef _WIN32
#include<windows.h>
#endif
using namespace std;
template<class T>void read(T &x){
   x=0;int f=0;char ch=getchar();
   while(ch<'0'||ch>'9') {f|=(ch=='-');ch=getchar();}
   while(ch>='0'&&ch<='9'){x=(x<<1)+(x<<3)+(ch^48);ch=getchar();}
   x=f?-x:x;
}
#define int long long
const int N=5e5;
int n,m,t1[N],t2[N],num[N],a[N];
inline void insert(int x,int y1,int y2)
{
    for(int i=x;i<=n+1;i+=(i)&(-i))
    {
        t1[i]+=y1;
        t2[i]+=y2;
    }
}
inline int query1(int x)
{
    int ans=0;
    for(int i=x;i>0;i-=(i)&(-i)) ans+=t1[i];
    return ans;
}
inline int query2(int x)
{
    int ans=0;
    for(int i=x;i>0;i-=(i)&(-i)) ans+=t2[i];
    return ans;
}
int opt,k,x;
signed main()
{
    read(n),read(m);
    for(int i=1;i<=n;i++) 
    {
        read(a[i]);
        num[i]=query2(n)-query2(a[i]);
        insert(a[i],num[i],1);
    }
    memset(t1,0,sizeof(t1));
    memset(t2,0,sizeof(t2));
    for(int i=1;i<=n;i++) insert(num[i] +1,num[i],1);
    for(int i=1;i<=m;i++)
    {
        read(opt),read(x);
        if(opt==1)
        {
           // printf("%lld %lld\n",num[x],num[x+1]);
            insert(num[x] +1,-num[x],-1);
            insert(num[x+1] +1,-num[x+1],-1);
            if(a[x]<a[x+1])
            {
                int vx=num[x],vx1=num[x+1];
                insert(num[x+1] +1,num[x+1],1);
                insert(num[x]+1 +1,num[x]+1,1);
                num[x]=vx1;
                num[x+1]=vx+1;
            }
            else
            {
                int vx=num[x],vx1=num[x+1];
                insert(num[x+1]-1 +1,num[x+1]-1,1);
                insert(num[x] +1,num[x],1);
                num[x]=vx1-1;
                num[x+1]=vx;
            }
            swap(a[x],a[x+1]);
        }
        else
        {
            if(x>=n){puts("0");continue;}
            int frt=query1(n +1)-query1(x-1 +1);
            int mins=query2(n +1)-query2(x-1 +1);
            mins*=x;
            printf("%lld\n",(frt-mins)<0?0:frt-mins);
        }
        
    }
    #ifdef _WIN32
    system("pause");
    #endif
}
```