---
title: 群论学习笔记-Part2
tags: Group-Theory
layout: article
license: true
toc: true
key: a20210710
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
# 点群操作基函数
## 球谐函数
对于点群操作,可以找到对应的一些基函数来满足变换性质,从而在基函数的基础上可以得到操作的矩阵表示,这里就以球谐函数为出发点,来寻找点群操作的基函数.首先球谐函数的定义为

$$Y_l^m(\theta,\phi)=\sqrt{\frac{(2l+1)(l-\rvert m\rvert)!}{4\pi(l+\rvert m\rvert)!}}P_l^m(\cos\theta)\exp(im\phi)$$

这里$P_l^m(\cos\theta)$是勒让德函数

$$P_l^m(\cos\theta)=\frac{1}{2^ll!}\sin^{\rvert m\rvert}\theta\frac{d^{l+\rvert m\rvert}}{(d\cos\theta)^{l+\rvert m\rvert}}\{(\cos^2\theta-1)^l\}$$

一个转动操作$R$可以通过欧拉角($\alpha,\beta,\gamma$)来表示:首先进行绕z轴的主动转动角为$\alpha,(0\le\alpha\le2\pi)$,接下来绕着y轴进行主动转动$\beta,(0\le\beta\le\pi)$,最后绕着z轴主动转动$\gamma,(0\le\gamma\le 2\pi)$.在三维的求坐标系中,第一次转动$\alpha$对应着$(r,\theta,\phi)\rightarrow(r,\theta,\phi+\alpha)$,第二次转动$\beta$对应$(r,\theta,0)\rightarrow (r,\theta+\beta,0)$,第三次转动$\gamma$对应着$(r,\theta,\phi)\rightarrow (r,\theta,\phi+\gamma)$.

![png](/assets/images/GroupTheory/1-13.png)

一个转动操作$R(\alpha,\beta,\gamma)$就对应着连续进行这三个操作,这里采用主动坐标系(active),此时的转动方向都是逆时针方向进行的.当将一个转动操作作用到球谐函数上之后

$$R(\alpha,\beta,\gamma)Y^m_l(\theta,\phi)=\sum_{n=-l}^{l}Y^n_l(\theta,\phi)\mathcal{D}^l\{R(\alpha,\beta,\gamma)\}_{mn}$$

这里的矩阵$\mathcal{D}^l$为

$$\mathcal{D}^l\{R(\alpha,\beta,\gamma)\}_{nm}=C_{nm}\exp(-in\gamma)d^l(\beta)_{nm}\exp(-im\alpha),\quad C_{nm}=(i^{\rvert n\rvert+n})(i^{-\rvert m\rvert -m})$$

$$d^l(\beta)_{nm}=\sum_k\frac{(-1)^{k-m+n}\sqrt{(l+n)!(l+m)!(l-n)!(l-m)!}}{(l-n-k)!(l+m-k)!k!(k-m+n)!}\cos^{2l+m-n-2k}(\frac{1}{2}\beta)\sin^{2k+n-m}(\frac{1}{2}\beta),\quad k=\text{max}\{0,(m-n)\}\rightarrow\text{min}\{(l-n),(l+m)\}$$

对于三维空间中的转动操作$R(\alpha,\beta,\gamma)$,当整数$l$确定之后,只有唯一的一个$\mathcal{D}^l\{R(\alpha,\beta,\gamma)\}$与之相对应.对于一个给定的$l$值的矩阵$\mathcal{D}^l\{R(\alpha,\beta,\gamma)\}$形成了一个$(2l+1)$维的旋转群$R(\alpha,\beta,\gamma)$的表示,而球谐函数$Y_l^m(\theta,\phi)(-l\le m\le l)$则是这个表示的基矢.矩阵元素$d^l(\beta)_{nm}$会有下面的对称关系

$$d^l(\beta)_{nm}=d^l(\beta)_{-m,-n}=(-1)^{m+n}d^l(\beta)_{mn}$$

因此在计算$d^l(\beta)$的时候,只需要计算$-l\le m\le l,\rvert m\rvert\le n\le l$范围内的值即可.这里来主要关注$\beta=0,\frac{1}{2}\pi,\pi$处的性质,原因有两个:任意$\beta$角度下的值都可以被转换到$\beta=\frac{1}{2}\pi$计算,对于晶体点群操作,总可以选择一个合适的轴,将$\beta$角变为$0,\frac{1}{2}\pi,\pi$中的一个值.

- 当$\beta=0$的时候:

$$\mathcal{D}^l\{R(\alpha,0,\gamma)\}_{nm}=\exp(-im\alpha)\exp(-im\gamma)\delta_{nm}$$

- 当$\beta=\pi$的时候:

$$\mathcal{D}^l\{R(\alpha,\pi,\gamma)\}_{nm}=(-1)^l\exp(-im\alpha)\exp(im\gamma)\delta_{n,-m}$$

为了研究球谐函数在晶体点群操作下的性质,还需要考虑反演操作$I$

$$IY^l_m(\theta,\phi)=(-1)^lY^l_m(\theta,\phi)$$

下面给出一个点群操作对应的欧拉角

![png](/assets/images/GroupTheory/1-14.png)

## 基函数寻找
对弈一个群$\mathbf{G}$其对应的阶数为$\rvert\mathbf{G}\rvert$,其对应的不可约表示$\Gamma^i\{R\rightarrow\mathbf{D}^i(R)\}$已知,这里的$\mathbf{D}^i$是是群元$R$的矩阵表示,对应的维度是$d_i$,而现在就要找到一组合适的基矢$\langle\phi_1^i,\phi_2^i,\cdots,\phi_{d_i}^i\rvert$满足

$$R\phi_s^i=\sum_{t=1}^{d_i}\phi_t^i\mathbf{D}^i(R)_{ts},\quad R\in\mathbf{G}$$







