---
title: 拓扑10重分类表笔记
tags: Topology
layout: article
license: true
toc: true
key: a20210523
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

# Dirac 理论
## 拓扑等价/不等价
一个满足对称性的最小哈密顿量

$$H({\bf k})=m\gamma_0+\sum_{i=1}^Nk_i\gamma_i\label{eq1}$$

这里的$N$表示空间维度,$\gamma_i$是满足反对易关系的厄米矩阵,${\gamma_i,\gamma_j}=2\delta_{ij}$,而满足对称性即意味着,在一个g对称操作下

$$gH({\bf k})g^{-1}=H(g{\bf k})$$

最小哈密顿量的意思是取能够同时满足对称性和反对易关系的最小维度的矩阵.
{:.info}

哈密顿量(\ref{eq1})的能谱为

$$\pm\sqrt{m^2+{\bf k}^2}$$

显然$m>0$的所有态都是拓扑等价的,$m<0$的态也都是拓扑等价的,**如何判断$m>0$与$m<0$是否为拓扑等价?**

方法:在不扩大维度的情况下,来寻找一个额外的质量项,如果存在一个同纬度的矩阵$\tilde{\gamma}_0$,它与所有的$\gamma_i$都反对易,而且满足所有的对称性,那么就可以在原来的哈密顿量中增加一项$\tilde{m}_0\tilde{\gamma}_0$,从而能谱变为$\pm\sqrt{m^2+\tilde{m}_0^2+{\bf k}^2}$,此时当$m\rightarrow -m$进行演化的时候,只要保证$\tilde{m}_0\neq 0$,这个演化不会有能隙关闭的过程,是个绝热演化.相反的,如果不存在这样的质量项,当进行同样的演化过程的时候,由$m>0$到$m<0$必然会经历一次能隙的闭合,此时$m>0$与$m<0$是拓扑不等价的两个相.
{:.success}

# $\mathcal{Z}\quad\text{or}\quad \mathcal{Z}_2$
要判断拓扑相的拓扑分类是$\mathcal{Z}$还是$\mathcal{Z}_2$,**需要考察当把几个最小哈密顿量直和起来就可以加入额外的质量项**.比如,当把两个最小哈密顿量直和起来,就可以加入额外的质量项,则说明两个拓扑态的直和是个平庸态,那么它对应的拓扑分类就是$\mathcal{Z}_2$.

## Chern 绝缘体
以二维系统为例演示狄拉克理论的用法,二维情况下最小的Dirac模型为

$$H({\bf {)=m\sigma_z+k_x\sigma_x+k_y\sigma_y\label{eq2}$$

三个Pauli矩阵外加一个单位矩阵,可以构成二维矩阵的完备基矢,所以此时无法找到另外的$2\times 2$的厄米矩阵同时与三个Pauli矩阵都反对易.当把两个(\ref{eq2})直和起来之后,$\tau_0\otimes H({\bf k})$,此时仍然无法加入满足要求的质量项.如果把质量符号相反的最小模型直和起来,$\tau_z\otimes H({\bf k})$,此时就可以加入形如$\tau_x\sigma_0$的额外质量项.实际上,我们将任意多个质量同号的Chern剧院提直和起来,都不能加入额外的质量项;而每一对质量相反的Chern绝缘体之间总是可以加入额外的质量项,这索命无对称性的二维系统具有$\mathcal{Z}$的拓扑分量,其中拓扑不平庸的态统称为Chern绝缘体.

## 时间反演不变系统
这里分析时间反演不变的二维系统,$\mathcal{T}=-1$,假设时间反演操作为$\mathcal{T}=-i\sigma_y\mathcal{K}$,那么一个满足对称性的最小哈密顿量为

$$H({\bf k})=m\tau_y\sigma_z+k_x\tau_0\sigma_x+k_y\tau_0\sigma_y$$

此时可以加入的反对易质量项为$\tau_x\sigma_z,\tau_z\sigma_z$,但是这两项都破坏了时间反演对称,所以此时并不存在额外的质量项,可以在满足对称性的条件下仍然和(\ref{eq3})中的每一项都反对易.接下来考虑两个最小模型的直和形式,$\mu_0\otimes H({\bf })$,可以发现此时可以加入形如$\mu_y\otimes\tau_x\sigma_z$的项,既满足对称性要求同时和所有的$\gamma$矩阵满足反对易关系.而对于质量相反的直和形式$\mu_z\otimes H({\bf k})$可以加入$\mu_x\tau_0\sigma_0$这样的额外质量项.由此可以得到时间反演不变的二维系统的拓扑分类是$\mathcal{Z}_2$.虽然此时无法加入满足时间反演不变的质量项,但是却可以加入破坏时间反演的质量项,这说明$\mathcal{Z}_2$分类中不平庸的态在破缺时间反演之后会变成平庸态,因此这个态被称为时间反演保护的拓扑绝缘体.

# 参考
- 1.拓扑半金属的磁响应与拓扑绝缘体中的$d-2$为边界态






