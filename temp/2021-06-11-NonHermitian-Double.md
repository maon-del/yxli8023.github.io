---
title: 两维非厄米体系中的Fermion Doubling Theorems
tags: Topology Non-Hermitian
layout: article
license: true
toc: true
key: a202106010
pageview: true
header:
  theme: dark
  background: 'linear-gradient(135deg, rgb(34, 139, 87), rgb(139, 34, 139))'
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
aside:
    toc: true
sitemap: true
mathjax: true
author: YuXuan
show_author_profile: true
---
这篇博客想通过精读一片研究两维非厄米体系中的Fermion Doubling Theorems的PRL文章,同时了解厄米与非厄米体系中的Fermion Doubling Theorems到底是什么.
{:.info}
<!--more-->
在学习凝聚态中的拓扑的时候,总是看到Weyl点是要成对出现的(不过也有了一些材料研究,可以让Weyl点单独出现),这是背后由比较深刻的物理,涉及格点规范场论,暂时功力不够看不懂,我还没有完全理解,因为相关的文章比较老;不过最近在活跃的非厄米体系中开始研究Fermion Doubling Theorems问题,我感觉和Weyl点成对出现是有关联的,所以准备借这篇非厄米的文章来学习一下这个概念,**如有大佬清楚这里面的联系,还请不吝赐教**.
# Fermion doubling
`当简单得尝试将一个费米子场放置到格点上的时候,就会出现一些虚假的状态,这样一来,每个原始的费米子会出现2d个费米子粒子,这里d是系统的维度.`
下面利用凝聚态的语言理解一下,假定是利用连续模型来描述能带,那么在$\Gamma=(0,0)$的时候,模型是个massless的Dirac方程,在这个点就有Dirac费米子,当把连续模型变成紧束缚模型之后,就会把原本的无限大的空间$k\rightarrow+\infty$限制到第一布里渊区中,假定是正方点整,那么在布里渊区中的每个角落处于中心$\Gamma$点是等价的,此时在这些点上再对紧束缚模型做低能展开,同样可以得到连续模型,只不过此时前面的系数会出现一个负号,或者不出现负号,也就是说在格点模型上Fermion的数目不再是一个了,这也就是Fermion doubling.
## Mathematica overview
在$d$维的时候考虑质量为$m$的自由Dirac费米子,其作用量为

$$S=\int d^dx\bar{\psi}(i\gamma_\mu a^\mu-m)\psi$$

这里的$\gamma_\mu$就是gamma矩阵,当把这个作用量离散化到立方格点上之后,费米子场$\psi(x)$就变成了离散的形式$\psi_x$,此时的$x$表示的是格点位置.而原本的导数则变成有限差分,作用量变为

$$S=a^d\sum_{x,\mu}\frac{i}{2a}(\bar{\psi}_x\gamma_\mu\psi_{x+\hat{\mu}}-\bar{\psi}_{x+\hat{\mu}}\gamma_\mu\psi_x)-a^d\sum_{x}m\bar{\psi}_x\psi_x$$

这里的$a$是格点间距,$\hat{\mu}$是沿着$\mu$方向的单位矢量,当在动量空间中计算时

$$S^{-1}(p)=m+\frac{i}{a}\sum_\mu\gamma_\mu\sin(p_\mu a)$$

因为实空间中的格点间距$a$是有限的,则动量$p_\mu$限制在布里渊区中,通常取第一布里渊区$[-\pi/a,\pi/a]$.

在$S^{-1}$中令$a\rightarrow 0$的时候,就可以得到正确的连续模型下的结果,但是当在布里渊区角落($\pi/2$)处展开这个表达式的时候,可以发现同样会得到连续模型的结果,只不过此时会在gamma矩阵前面发生符号改变.这也就一维着,当动量的某一个分量在$\pi/a$附近的时候,离散的费米子场的行为同样会与连续情形下的费米子相同,这可以发生在动量空间动量的所有$d$个分量上,相比于原来连续模型的Dirac费米子,这里会有$2^d$中不同"味道"的费米子.




# 参考
- 1.[Fermion Doubling Theorems in Two-Dimensional Non-Hermitian Systems for Fermi Points and Exceptional Points](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.126.086401)
- 2.[Fermion doubling](https://en.wikipedia.org/wiki/Fermion_doubling)

