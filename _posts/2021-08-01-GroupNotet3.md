---
title: 群论学习笔记-Part3
tags: Group-Theory
layout: article
license: true
toc: true
key: a20210801
cover: /assets/images/GroupTheory/cube_symmetry.jpg
header:
  theme: dark
  background: 'linear-gradient(135deg, rgb(34, 139, 87), rgb(139, 34, 139))'
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
pageview: true
sitemap: true
mathjax: true
author: YuXuan
show_author_profile: true
---
学习群论有一段时间了, 这里想结合一些工具, 并通过一些书籍阅读来将自己所学到的内容整理一下, 同时加深一下自己对这些知识内容的理解.
{:.info}
<!--more-->
# 空间群
空间群$\mathbf{G}$包含了纯平移操作$\{E\rvert\mathbf{t}\}$,这些平移操作构成了空间群$\mathbf{G}$的一个不变子群$\mathbf{T}$.

$$\mathbf{t}=n_1\mathbf{t}_1+n_2\mathbf{t}_2+n_3\mathbf{t}_3$$

对于实际的晶体,通常考虑周期性边界条件

$$\{E\rvert l_1N_1\mathbf{t}_1+l_2N_2\mathbf{t}_2+l_3N_3\mathbf{t}_3\}=\{E\rvert\mathbf{O}\}$$

对于一个晶体,如果存在两个布拉菲点阵,那么它们之间一定是等价的,通过连续形变,一定可以将两者进行相互变换,而且在变换过程中要始终保证点阵的对称性是相同的,不能改变其对称性.下面给出14中布拉菲点阵的基矢及相关信息

![png](/assets/images/GroupTheory/3-1.png)

![png](/assets/images/GroupTheory/3-2.png)

![png](/assets/images/GroupTheory/3-3.png)

每个晶系满足的对称操作如下

![png](/assets/images/GroupTheory/3-4.png)

下面给出每个对称操作对布拉菲点阵基矢的变换关系

![png](/assets/images/GroupTheory/3-5.png)

![png](/assets/images/GroupTheory/3-6.png)

![png](/assets/images/GroupTheory/3-7.png)

![png](/assets/images/GroupTheory/3-8.png)

同样可以利用[SpaceGroupIrep](https://github.com/goodluck1982/SpaceGroupIrep)这个工具来得到具体的表

![png](/assets/images/GroupTheory/3-9.png)

通过实空间的布拉菲点阵,同样可以定义出倒空间中的点阵

$$\mathbf{g}_i\cdot\mathbf{t}_j=2\pi\delta_{ij},\quad (i,j=1,2,3)$$

利用上面的关系可以得到倒空间的基矢为

$$\mathbf{g}_1=\frac{2\pi(\mathbf{t}_2\times\mathbf{t}_3)}{\mathbf{t}_1\cdot(\mathbf{t}_2\times\mathbf{t}_3)},\quad\mathbf{g}_2=\frac{2\pi(\mathbf{t}_3\times\mathbf{t}_1)}{\mathbf{t}_2\cdot(\mathbf{t}_3\times\mathbf{t}_1)},\quad\mathbf{g}_3=\frac{2\pi(\mathbf{t}_1\times\mathbf{t}_2)}{\mathbf{t}_3\cdot(\mathbf{t}_1\times\mathbf{t}_2)}$$

利用这些基矢,可以在倒空间中定义点阵

$$\mathbf{g}=n_1\mathbf{g}_1+n_2\mathbf{g}_2+n_3\mathbf{g}_3$$

倒空间中的布拉菲点阵如下

![png](/assets/images/GroupTheory/3-15.png)

同样的也可以得到点群操作对倒空间基矢的变换关系

![png](/assets/images/GroupTheory/3-10.png)

![png](/assets/images/GroupTheory/3-11.png)

![png](/assets/images/GroupTheory/3-12.png)

![png](/assets/images/GroupTheory/3-13.png)

利用**SpaceGroupIrep**来得到

![png](/assets/images/GroupTheory/3-14.png)

## The classification of points and lines of symmetry
三维空间中红一共有14种不同的布拉菲点阵,但是有的点阵只有一种布里渊区,有的点阵可以有几种不同形式的布里渊区,讲这些所有的布里渊区集合到一起,总共有22中布里渊区,如下所示

![png](/assets/images/GroupTheory/3-16.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-17.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-18.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-19.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-20.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-21.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-22.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-23.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-24.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-25.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-26.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-27.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-28.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-29.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-30.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-31.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-32.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-33.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-34.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-35.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-36.png){:width="330px",:height="495px"}

![png](/assets/images/GroupTheory/3-37.png)









