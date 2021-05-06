---
title: 拓扑10重分类表笔记
tags: Topology
layout: article
license: true
toc: true
key: a20210209
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
这里整理一下最近看拓扑分类文章时候的一些笔记.
<!--more-->
最近在做一些工作,在阅读文献的时候有一些比较重要的工作需要仔细的阅读和理解,这里我就想把自己看拓扑分类这方面的文章时的一些理解和笔记整理一下,也可以加深自己对文章的理解.
# 10重分类
![png](/assets/images/topology/AT-ten.png)

这是根据手性对称(sublattice symmetry or chiral symmetry),时间反演对称(Time reversal symmetry),粒子空穴对称(Particle hole symmetry)对哈密顿量进行分类,首先来理解一下为什么会有10个分类.

首先TRS与PHS都是反对易操作算符,可以写作$\hat{U}\hat{\mathcal{K}}$,其中$\hat{U}$是个幺正操作,$\hat{\mathcal{K}}$是复数共轭操作.TRS与PHS的"本征值"都可以是$-1,+1,0$这三种选择,$0$则代表没有这种对称性,$\pm 1$则代表将这个算符对单粒子算符作用两次之后是$+1$还是$-1$,所以它们两个的组合共有$9$种不同的结果.手性对称(SLS)可以由这两种对称性组合出来

$$SLS=TRS\times PHS$$

所以由TRS与PHS确定的9个组合种,其中的8个可以通过SLS的有无来确定,而唯一无法确定的就是第9个$(TRS,PHS)=(0,0)$这种情况,此时两种对称性都不存在,**但是却可以存在SLS或者不存在SLS**,这又会有两种情况,所以加上前面的8种情况,就一共有10种分类.

> 上面表种后面三列代表着10重分类下,不同空间维度标志其拓扑性质不变量的形式.$Z$表示整数,$Z_2$则表示$\{-1,+1\}$

# 对称操作算符
这里存在两种类型的对称操作算符

$$\begin{equation}
\begin{aligned}
&P:\mathcal{H}=-P\mathcal{H}P^{-1},\quad PP^\dagger=1,\quad P^2=+1\\
&C:\mathcal{H}=\epsilon_cC\mathcal{H}^{T}C^{-1},\quad CC^\dagger=1,\quad C^T=\eta_c C
\end{aligned}
\end{equation}$$

对于$C$类型的算符$\epsilon_c=1$代表TRS算符,$\epsilon_c=-1$代表PHS算符.

$\eta_c=\pm 1$:$(\epsilon_c,\eta_c)=(1,1)$则代表spinless(整数自旋)的TRS算符,$(\epsilon_c,\eta_c)=(1,-1)$代表spinfull(自旋$\frac{1}{2}$)的TRS算符.同样的$(\epsilon_c,\eta_c)=(-1,1)$表示PHS自旋三重态的BdG哈密顿量,$(\epsilon_c,\eta_c)=(-1,-1)$表示PHS自旋单重态BdG哈密顿量.

如果存在PHS,则系统的能量一定是关于零对称分布的.
{:.warning}

在动量空间中,哈密顿量$H(\mathbf{k})$在这些算符的操作下变换为

$$\begin{equation}\begin{aligned}
&\mathcal{T}H(\mathbf{k})\mathcal{T}=H(-\mathbf{k})\qquad TRS\\
&\mathcal{C}H(\mathbf{k})\mathcal{C}=-H(-\mathbf{k})\qquad PHS\\
&\mathcal{S}H(\mathbf{k})\mathcal{S}=-H(\mathbf{k})\qquad \textrm{Chiral Symmetry}\\
\end{aligned}\end{equation}$$




