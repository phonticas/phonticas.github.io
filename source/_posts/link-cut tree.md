---
title: link-cut-tree
author: Protons
avatar: 'https://cdn.jsdelivr.net/gh/protons-z/cdn@6.3.0/images/profile/head.jpg'
authorLink: 
authorAbout: 
authorDesc: 
categories: 笔记
comments: true
date: 2020-07-22 23:43:11
tags: link-cut-tree
keywords:
description:
photos: https://cdn.jsdelivr.net/gh/protons-z/cdn@6.1.6/img/333580.jpg
mathjax: true
---
link-cut tree 顾名思义 可以支持树上的动态操作

而其主要是如何通过splay来表示原树

lct 亦称实链剖分
我们使用一颗splay来维护一条实链,splay里点的权便是该点在原树中的深度

---

直入主题，怎么通过splay的变化来反映原树的变化

### 操作

1. 重中之重 access(x)操作，即打通一条均是实链的从x到原树的根的路径。
因为是打通根到x的路径，所以x一定在打通后的实链的链底。
那么我们想一下由于是实链的底，深度一定最大，所以splay(x)到根后，x深度一定比链上所有节点深度大。
所以现在splay上x的所有儿子都在其左子树上（左子树<根<右子树）。
而此时现在splay上x的根边是在原树上现在这条实链的链顶的父亲。
因为lct中spaly上认父不认子，所以我们可以直接找到链顶的父亲f，考虑它(f)也是这个实链的链底，所以我们也对f进行类似刚刚对x的操作。
先将f,splay到根，然后f左子树只剩下它原先的实儿子和其(实儿子)下子。
此时我们便把f右儿子直接换成x,由于虚边认父不认子，原先的实儿子变虚，x变实儿子。
继续进行该操作直到到达根节点。
``` cpp
inline void access(int x)
{
    for(int y=0;x;y=x,x=fa[x])
    {
        splay(x); // 把x旋到根
        t[x].son[1]=y; //更改右儿子（右子树）
        pushup(x); // 更新结点
    }
}
```

2. makeroot(x) 操作，将x换成原树的根。
我们考虑怎么做，首先，对x先打通一条到根的路径（access(x)）。
此时因为x是这个实链的底，深度最大，所以把此时的x,splay到根，那么，x的右子树便是空的。
假如我们把x提到原树的根，那么显然对于原先结点 $k$,$dep_k=dep_x-dep_k$ 。
我们可以看出这个把符号 `>` 转换成 `<` ，也就是把splay的左右子树反转。
在文艺平衡树中我们通过打标记和pushdown一系列操作进行区间翻转。
``` cpp
inline void makeroot(int x)
{
    access(x);
    spaly(x);
    t[x].rev=1;
}
```

3. findroot(x) 操作，找出x原树的根（lct维护的可以是森林）。
怎么做？因为根的dep最小，所以我们类似makeroot(x)中先access(x),再splay(x)使得x为splay根。
然后一直找左儿子（左儿子<根<右儿子） ，最后的既为根。

``` cpp
inline int findroot(int x)
{
    access(x);splay(x);
    while(t[x].son[0]) x=t[x].son[0];
    return x;
}
```

4. link(x,y) 操作在原树上连接(x,y)。
怎么做？我们考虑(x,y)原先一定不联通（因为lct只能维护树）。
所以现在我们要先判断 $[findroot(x)=findroot(y)]$。
其次，我们先把x换到原树那个根，然后因为是根所以他没有爸爸。
我们考虑加一条虚边从 $x->y$因为是虚边，y的形态不改变，而x是原树的根把他的爸爸改成y对他的子树无影响。
所以就可以直接连虚边，来进行link操作。
``` cpp
inline void link(int x,int y)
{
    makeroot(x);
    fa[x]=y;
}
```
5. split(x,y) 操作在原树上提取从(x->y) 这条链。
我们可以先把x换成根（makeroot(x)）,然后直接打通y到根的路径（access(y)），然后只要把y splay到根就可以直接查询这条链的信息！
``` cpp
inline void split(int x,int y)
{
    makeroot(x);
    access(y);
    splay(y);
}
```
6. cut(x,y) 操作在原树上断掉$(x->y)$ 这条边。
我们先提取出来(x,y)这条边(split(x,y))，然后因为(x,y)是相连的。$dep_x=dep_y-1$
显然，假如y是根，x就是y的左儿子，我们自然可以直接把y的左儿子改成虚的，也就是不要了，x的父亲也不认。（这并不是虚边认父不认子）
``` cpp
inline void cut(int x,int y)
{
    split(x,y);
    if(t[y].son[0]==x) t[y].son[0]=0;
}
```