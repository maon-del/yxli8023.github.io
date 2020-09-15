---
title: Schrodinger,Heisenberg,Interaction绘景的区别与联系
tags: Method Study
layout: article
license: true
toc: true
key: a20200915
pageview: true
sitemap: true
mathjax: true
author: YuXuan
show_author_profile: true
---
在量子力学进一步的学习中,通常会遇到Schrodinger,Heisenberg,Interaction这三种绘景,在处理不同的问题时,如果选取的绘景合适,那么问题的处理会较为方便,这里合适的绘景只是可以让问题变得容易处理,本质上三种不同的绘景所得到的结果都是相同的,在这里就把三种不同绘景之间的联系与区别进行整理,并整理自己的一些经验和理解.
{:.info}
<!--more-->
# Schrodinger绘景
最初学习量子力学的时候,接触的其实就是Schrodinger绘景,在自然单位制下的薛定谔方程为

$$i\frac{\partial}{\partial t}\psi(t)=H\psi(t)$$

$H$是体系的哈密顿量,$\psi$则是体系的波函数,上述方程的解为$\psi(t)=e^{-iHt}\psi(0)$.在Schrodinger绘景中可以看到,波函数是跟时间相关的,而算符H则是与时间无关的,且波函数的时间依赖仅仅是在$e^{-iEt}$中.

# Heisenberg绘景
Heisenberg绘景和Schrodinger绘景的区别就是现在波函数是与时间无关的,而算符则是和时间相关的

$$O(t)=e^{iHt}O(0)e^{-iHt}$$

上式中H是系统完整的哈密顿量,其中可以包含相互作用等其它外部影响.算符$O(0)$则可以认为就是Schrodinger绘景中的算符,也就是说0时刻的Heisenberg绘景中的算符就是Schrodinger绘景中的算符,而之后的时刻就不是了,因为Schrodinger绘景中的算符是与时间无关的,而对应的,此时波函数就是一个与时间无关的量,即Heisenberg绘景中波函数$\psi(0)$就是Schrodinger绘景中0时刻的波函数$\psi(0)$.对含时间的算符求导,即得到Heisenberg绘景下的运动方程

$$i\frac{\partial}{\partial t}O(t)=[O(t),H]$$

下面对算符在Heisenberg绘景中求期望值,将两个绘景中联系起来

$$\langle\psi^\dagger_1(t)O(0)\psi_2(t)\rangle=\langle\psi^\dagger_1(0)e^{iHt}O(0)e^{-iHt}\psi_2(0)\rangle$$

$$\langle\psi^\dagger_1(0)O(t)\psi_2(0)\rangle=\langle\psi^\dagger_1(0)e^{iHt}O(0)e^{-iHt}\psi_2(0)\rangle$$

通过上面两个公式可以看到,虽然是不同的表象,但是算符的期望值是相同的,结果一致

# Interaction绘景
相互作用绘景通常在格林函数的计算中有很大的用途,首先将哈密顿量分解为两部分

$$H = H_0 + V$$

分解成两部分之后$H_0$是无相互作用部分,$V$则是系统的相互作用部分.通常情况下$H_0$部分的哈密顿量是可以精确求解的,在相互作用绘景中通过这个可以精确求解的本征态来计算加入相互作用之后系统的各种性质.在相互作用绘景中,算符和波函数都是和时间相关的,下面就构造相互作用绘景下的算符和波函数.

$$\hat{O}(t)=e^{iH_0t}Oe^{-iH_0t}$$

这里强调一下,此时构造时间依赖的算符时利用的是无相互作用$H_0$,这与Heisenberg绘景是不同的,在Heisenberg绘景中构造时间依赖的算符的时候,利用的是系统完整的哈密顿量$H = H_0 + V$.相互作用绘景中的波函数为

$$\hat{\psi}(t)=e^{iH_0t}e^{-iHt}\psi(0)$$

在这里加一个算符的性质$e^Ae^B=e^{A+B}$成立的条件是$[A,B]=0$,因为这里处理的是算符,所以算符的指数关系并不和普通数的指数关系相同.

下面计算在相互作用绘景中算符的期望值

$$\langle\hat{\psi}^\dagger_1(t)\hat{O}(t)\hat{\psi}_2(t)\rangle=\langle\psi_1^\dagger(0)e^{iHt}e^{-iH_0t}(e^{iH_0t}Oe^{-iH_0t})e^{iH_0t}e^{-iHt}\psi_2(0)\rangle\\
=\langle\psi^\dagger(0)e^{iHt}O(0)e^{-iHt}\psi_2(0)\rangle$$

在相互作用绘景中的期望值计算又和Schrodinger绘景中的计算完全一致,所以这三种不同的绘景只是用来简化问题的处理,实际的计算中结果是完全相同的.
对相互作用绘景波函数求时间的导数可得

$$\frac{\partial}{\partial t}\hat{\psi}(t)=ie^{iH_0t}(H_0-H)e^{-iHt}\psi(0)=-ie^{iH_0t}Ve^{-iHt}\psi(0)=-ie^{iH_0t}Ve^{-iH_0t}[e^{iH_0t}e^{-iHt}\psi(0)]$$

$$\frac{\partial}{\partial t}\hat{\psi}(t)=-i\hat{V}(t)\hat{\psi}(t)$$

从上面的方程可以看到,波函数满足一个和$\hat{V}(t)$相关的微分方程.

接下来介绍相互作用绘景中的时间演化算符**$U(t)=e^{iH_0t}e^{-iHt}$**,显然当$t=0$时,$U(0)=1$,对时间演化算符求时间导数后

$$\frac{\partial}{\partial t}U(t)=ie^{iH_0t}(H_0-H)e^{-iHt}=-ie^{iH_0t}V(e^{-iH_0t}e^{iH_0t})e^{-iHt}=-i\hat{V}(t)U(t)$$

时间演化算符也满足和相互作用绘景中的波函数满足同样的微分方程,求解这个微分方程可得

$$U(t)-U(0)=-i\int^t_0dt_1\hat{V}(t_1)U(t_1)$$

利用前面$t=0$时刻的条件后:$U(t) = 1-i\int^t_0dt_1\hat{V}(t_1)U(t_1)$

从这个微分方程的解可以看到,这是一个关于$U(t)$的迭代方程,通过重复的回代,可以得到一个无穷多项的结果

$$U(t)=1-i\int^t_0dt_1\hat{V}(t_1)+(-i)^2\int^t_0dt_1\int^t_0dt_2\hat{V}(t_1)\hat{V}(t_2)+\dots\\
=\sum_{n=0}^\infty(-i)^n\int^t_0dt_1\int^t_0dt_2\dots\int^{t_{n-1}}_0\hat{V}(t_1)\hat{V}(t_2)\dots\hat{V}(t_n)$$

## 编时算符
编时算符的引进目的,就是为了使得一些算符的作用是有意义的,而且可以使得一些公式在形式上可以写的很简单,使得在进行一些计算的时候很方便.编时算符通常是作用在一组与时间相关的算符上$T[\hat{V}(t_1)\hat{V}(t_2)\hat{V}(t_3)]$,编时算符作用之后展开为

$$T[\hat{V}(t_1)\hat{V}(t_2)\hat{V}(t_3)]=\hat{V}(t_3)\hat{V}(t_1)\hat{V}(t_2)\qquad if \quad t_3>t_2>t_1$$

编时算符的作用就是按照一定的时间顺序来将算符组织起来,使得时间较早的算符先作用,时间较后的算符后作用,这个是要符合因果律.


# 参考
1.Many Particle Physics(Mahan,Third edition)

