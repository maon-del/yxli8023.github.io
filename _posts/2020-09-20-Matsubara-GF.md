---
title: 松原格林函数与零温格林函数联系 
tags:  Study Method
layout: article
license: true
toc: true
key: a20200920
pageview: true
sitemap: true
mathjax: true
author: YuXuan
show_author_profile: true
---
格林函数的计算是在零温下进行的,但是实验却是再非零温下进行,那么就意味着实验观测中一定包含了热力学涨落,而这时候热力学统计物理这个工具就可以发挥作用了,自然的就需要利用松原格林函数来对有限温系统的格林函数进行计算,而零温时候的结果仅仅就是松原格林函数进行解析延拓即可,这里就主要展示一下松原格林函数的一些推导以及它与零温格林函数的联系是如何建立起来的.
{:.info}
<!--more-->
# 热力学平均
首先定义关联函数

$$C_{AB}(t,t')=-\langle A(t)B(t')\rangle$$

在这里$\langle\dots\rangle$是求期望值,如果是在非零温的情况下,那么求其统计平均为

$$C_{A B}\left(t, t^{\prime}\right)=-\frac{1}{Z} \operatorname{Tr}\left(e^{-\beta H} A(t) B\left(t^{\prime}\right)\right)\label{eq1}$$

$Tr\equiv\sum_n\langle n\rvert\dots\rvert n\rangle$是一组完备基矢上的求和,接下来将(\ref{eq1})改写到相互作用绘景下,相互作用绘景的内容可以参考[Schrodinger,Heisenberg,Interaction绘景的区别与联系](https://yxli8023.github.io/2020/09/15/picture-compare.html)这篇博客

$$C_{A B}\left(t, t^{\prime}\right)=-\frac{1}{Z} \operatorname{Tr}\left[e^{-\beta H} \hat{U}(0, t) \hat{A}(t) \hat{U}\left(t, t^{\prime}\right) \hat{B}\left(t^{\prime}\right) \hat{U}\left(t^{\prime}, 0\right)\right]$$

在[Schrodinger,Heisenberg,Interaction绘景的区别与联系](https://yxli8023.github.io/2020/09/15/picture-compare.html)中也提及到,利用相互作用绘景可以把有相互作用系统的基态与它无相互作用时的基态通过演化算符联系起来,从而达到在无相互作用基态上对物理量的求解,而这里进行这样的操作也是为了同样的目的.
# 虚时Heisenberg/Interaction 绘景
在这里再介绍一些虚时情况下的两种绘景.首先引进虚时完全就是一个数学的操作,是为了将统计物理中的$e^{\beta H}$与量子力学中的时间演化算符$e^{iHt}$在形式上可以进行统一,因为此时看上取好像一个是实数,另外一个则是复数,在进行$t\rightarrow i\tau$的变换后,此时$\tau$就是虚时间,那么从形式上来看$e^{\tau H}$和$e^{\beta H}$就都是实数的样子,而且这个时候也将温度$\beta=\frac{1}{k_B T}$和虚时间$it=\tau$联系了起来,这一点在松原格林函数中还是很重要的,具体它们之间是如何限制将在后面松原格林函数的性质讨论时展示.

在实时间Heisenberg绘景中

$$A(t)=e^{i t H} A e^{-i t H}$$

进行虚时变换之后

$$A(\tau)=e^{\tau H} A e^{-\tau H}$$

对应的相互作用绘景中的算符在虚时间下表示为

$$\hat{A}(\tau)=e^{\tau H_{0}} A e^{-\tau H_{0}}$$

**这里再次强调一下,这里的$H_0$是无相互作用时系统的哈密顿量**.

有了上面的这些关系之后,那么同样可以将虚时Heisenberg算符改写成虚时Interaction绘景中的形式

$$A(\tau) B\left(\tau^{\prime}\right)=\hat{U}(0, \tau) \hat{A}(\tau) \hat{U}\left(\tau, \tau^{\prime}\right) \hat{B}\left(\tau^{\prime}\right) \hat{U}\left(\tau^{\prime}, 0\right)\label{eq4}$$

虚时Interaction绘景下,演化算符为

$$\hat{U}\left(\tau, \tau^{\prime}\right)=e^{\tau H_{0}} e^{-\left(\tau-\tau^{\prime}\right) H} e^{-\tau^{\prime} H_{0}}\label{eq2}$$

$$\begin{aligned}
\hat{U}\left(\tau, \tau^{\prime}\right) &=\sum_{n=0}^{\infty} \frac{1}{n !}(-1)^{n} \int_{\tau^{\prime}}^{\tau} d \tau_{1} \cdots \int_{\tau^{\prime}}^{\tau} d \tau_{n} T_{\tau}\left(\hat{V}\left(\tau_{1}\right) \cdots \hat{V}\left(\tau_{n}\right)\right) \\
&=T_{\tau} \exp \left(-\int_{\tau^{\prime}}^{\tau} d \tau_{1} \hat{V}\left(\tau_{1}\right)\right)
\end{aligned}\label{eq3}$$

这里只是简单的将$it\rightarrow\tau$,其余的推导过程与[Schrodinger,Heisenberg,Interaction绘景的区别与联系](https://yxli8023.github.io/2020/09/15/picture-compare.html)中完全一致,就不做重复了.结合(\ref{eq2})和(\ref{eq3})之后,可以将热力学统计的因子$e^{\beta H}$进行改写

$$e^{-\beta H}=e^{-\beta H_{0}} \hat{U}(\beta, 0)=e^{-\beta H_{0}} T_{\tau} \exp \left(-\int_{0}^{\beta} d \tau_{1} \hat{V}\left(\tau_{1}\right)\right)$$

在虚时下同样可以有算符的热力学平均

$$\left\langle T_{\tau} A(\tau) B\left(\tau^{\prime}\right)\right\rangle=\frac{1}{Z} \operatorname{Tr}\left[e^{-\beta H} T_{\tau} A(\tau) B\left(\tau^{\prime}\right)\right]$$

利用(\ref{eq4})其在相互作用绘景下的形式可得

$$\left\langle T_{\tau} A(\tau) B\left(\tau^{\prime}\right)\right\rangle=\frac{1}{Z} \operatorname{Tr}\left[e^{-\beta H_{0}} \hat{U}(\beta, 0) T_{\tau}\left(\hat{U}(0, \tau) \hat{A}(\tau) \hat{U}\left(\tau, \tau^{\prime}\right) \hat{B}\left(\tau^{\prime}\right) \hat{U}\left(\tau^{\prime}, 0\right)\right)\right]$$

这里利用$Tr$的轮换不变性$Tr[ABC\dots YZ]=Tr[BC\dots YZA]$以及$\hat{U}\left(\tau, \tau^{\prime \prime}\right) \hat{U}\left(\tau^{\prime \prime}, \tau^{\prime}\right)=\hat{U}\left(\tau, \tau^{\prime}\right)$,以及$Z=\operatorname{Tr}\left[e^{-\beta H}\right]=\operatorname{Tr}\left[e^{-\beta H_{0} \hat{U}(\beta, 0)}\right]$可以得到

$$\left\langle T_{\tau} A(\tau) B\left(\tau^{\prime}\right)\right\rangle=\frac{1}{Z} \operatorname{Tr}\left[e^{-\beta H_{0}} T_{\tau} \hat{U}(\beta, 0) \hat{A}(\tau) \hat{B}\left(\tau^{\prime}\right)\right]=\frac{\left\langle T_{\tau} \hat{U}(\beta, 0) \hat{A}(\tau) \hat{B}\left(\tau^{\prime}\right)\right\rangle_{0}}{\langle\hat{U}(\beta, 0)\rangle_{0}}$$

从上面的结果可以看到,在虚时绘景下,由成功的把问题转换到了在无相互作用哈密顿量本征态上的计算.

# 松原格林函数的定义
