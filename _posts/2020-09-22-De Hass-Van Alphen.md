---
title: 德.哈斯-范.阿尔芬(De Hass-Van Alphen)效应
tags: Study
layout: article
license: true
toc: true
key: a20200922
pageview: true
sitemap: true
mathjax: true
author: YuXuan
show_author_profile: true
---
在固体物理的学习过程中,始终都要接触费米面这个概念,经常在学习理论知识,对实验的关注还是有些少,这里就整理一下实验上通过[De Hass-Van Alphen效应](https://en.wikipedia.org/wiki/De_Haas%E2%80%93van_Alphen_effect)测量费米面的一些理论知识,正好也梳理一下实验上的一些手法.
{:.info}
<!--more-->
# 电子在磁场中的运动
## 准经典分析
这里先从准经典角度整理一下电子点外加磁场中是如何运动的.

$$
\mathbf{v}(\mathbf{k})=\frac{1}{\hbar}\nabla_\mathbf{k}E(\mathbf{k})\\
\hbar\frac{d\mathbf{k}}{dt}=(-q)\mathbf{v}_k\times \mathbf{B}
$$

从上面的两个方程中可以有两个结论:
- 电子波矢$\mathbf{k}$沿着磁场方向是不随时间改变的,这点从第二个方程中可以得到,因为方程右端是速度和磁场的叉乘,结果中矢量的方向一定会同时垂直与速度和磁场的方向.


- 电子的能量$E(\mathbf{k})$是不会随时间变化的,也就是说电子始终在等能面上运动,这是因为磁场给电子的力是洛伦兹力,它是不会做功的,那么自然能量不会变化,电子就一直在等能面上运动.

## 量子分析
在不加磁场时,自由电子哈密顿量为$H=\frac{\mathbf{p}}{2m}=-\frac{\hbar^2}{2m}\nabla^2$,加入磁场之后,只要把动量$\mathbf{p}$替换成正则动量$\mathbf{p}+q\mathbf{A}$即可

$$H=\frac{1}{2m}(\mathbf{p}+q\mathbf{A})$$

假设磁场是沿着z方向的,取朗道规范$\mathbf{A}=(-By,0,0)$,则哈密顿量可以写成

$$H=\frac{1}{2m}[(\hat{p}_x-qBy)^2+\hat{p}_y+\hat{p}_z]$$

关于这个哈密顿量的求解可以参考固体物理$P_259$这也是一个标准的量子力学问题,最后可以求解得到随y变化部分波函数为

$$\varphi_n(y-y_0)\sim e^{-\frac{\omega_0}{2}(y-y_0)^2}H_n[\omega_0(y-y_0)]$$

这里$y_0=\frac{\hbar}{qB}k_x,\omega_0=\frac{qB}{m}$,这是一个中心在$y_0$,振动频率为$\omega_0$的谐振子波函数,$H_n$是厄密多项式.则最后总的波函数为$\psi=e^{i(k_xx+k_zz)}\varphi_n(y-y_0)$.上面的计算表明,在$x-y$平面内的圆周运动对应着一种简写运动,能量是量子化的,这些量子化的能级称谓朗道能级,$E=\frac{\hbar^2 k_z^2}{2m}+(n+\frac{1}{2})$.

# De Hass-Van Alphen效应


# 参考
- 1.固体物理(黄昆)