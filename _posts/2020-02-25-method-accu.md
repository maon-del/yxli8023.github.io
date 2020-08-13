---
title: 学习中方法技巧记录
tags: Study
layout: article
license: true
toc: true
pageview: true
aside:
    toc: true
sitemap: true
mathjax: true
author: YuXuan
show_author_profile: true
---
学习过程中的一些方法和技巧记录，脑袋是有限的，知识却永远学不完。
<!--more-->

# T矩阵方法介绍

纯净系统的哈密顿量为$H^0(\bf{k})$，加入杂质$V$后，系统的哈密顿量为$H(\bf{k}) = H^0(\bf{k}) + V$。

加入杂质后系统的格林函数为$$G = G^0 + G^0 T G^0$$，此处$G^0$代表纯净系统的格林函数:$G^0(z) = (z-H(\bf{k}))^{-1}$，$T$矩阵可以通过杂质$V$和$G^0$计算得到:$T=V(I-G^0V)^{-1}$，$I$代表单位矩阵。

对于点状杂质，通常是是写在实空间中的表达式$V(r)=V_0\delta(\bf{r})$，那么实空间中的格林函数为:$G(r,r') = G^0(r,r') + G^0(r,0)T_0(z)G^0(0,r')$，在实空间中局域的$T_0$矩阵为$T_0(z) = (V^{-1} - G^0(z))^{-1}$，$G^0(z)=\frac{1}{N}\sum_k(z-H_k^0)^{-1}$，它是纯净系统动量空间中的格林函数的傅里叶变换，公式中的N代表傅里叶变换时选取的k点的数目。

### 参考文献

> 1.[Impurity-induced states in conventional and unconventional superconductors]( https://journals.aps.org/rmp/abstract/10.1103/RevModPhys.78.373 )

# 实空间与k空间Fourier变换

在固体物理的研究中通常要使用到紧束缚近似模型，而且还会用到它的实空间和k空间Hamiltonian，通常取晶格常数a=1，则实空间与k空间算符的变换关系为

>  $c_{k}=\frac{1}{\sqrt{2\pi}}\sum_jc_je^{-ikj}$
>
> $c_j=\frac{1}{\sqrt{2\pi}}\int_{BZ}dkc_ke^{ikj}$

由于k空间是连续的，所以对动量k的积分是在整个第一布里渊区(BZ)进行的，而实空间的格点是离散的，所以由实空间算符到k空间算符进行的是离散的傅里叶变化，对应的由动量空间(k空间)到实空间的算符变化，进行的是连续傅里叶变换。

在此处需要说明的是，假设上面进行变换的算符都是费米子算符，则实空间与k空间的算符都是满足反对易关系的，在验证这个对易关系的时候，通常都要使用到$\delta$函数，它也同样有离散和连续的表达式

> $\sum_j\frac{1}{2\pi}e^{-i(k-k')j}=\delta(k-k')$
>
> $\frac{1}{2\pi}\int_{BZ}dke^{ik(x_i-x_j)}=\delta_{ij}$

若想将实空间中的Hamiltonian变换到k空间,则将$c_j$到$c_k$的变换关系代入,然后利用$\delta$函数的关系即可.同样的,由k空间变换到实空间的操作只不过是一个相反的过程,将本来的$c_k$写成由$c_j$的表示形式,然后利用$\delta$函数的关系即可.

通常,如果遇到实空间是个离散的晶格点阵,如果我们的体系在考虑的时候,并不是无限大的,那么对应着的k空间中的动量点k也是一些离散的量.假设取实空间的格点数为N,晶格常数为a,则实空间中系统的大小为L=N*a(为了简答考虑,先默认这个是一维的系统),则k点的取值为$k_m=\frac{2\pi m}{L}$,m的取值范围和N有关:$m=-\frac{N}{2},-\frac{N}{2}+1,...\frac{N}{2}-1$.这种离散的情况下通常进行实空间与动量空间变换时同样需要$\delta$函数的辅助

> $\frac{1}{N}\sum_ke^{-ikj}e^{-ikj'}=\delta_{jj'}$
>
> $\frac{1}{N}\sum_je^{ikj}e^{-ik'j}=\delta_{kk'}$

# 微分方程通解
$$H_{1}\left(-i \partial_{x}, k_{y}, k_{z}\right)=\left(\tilde{m}-\frac{t}{2} \partial_{x}^{2}+\frac{t}{2} k_{y}^{2}+\frac{t_{3}}{2} k_{z}^{2}\right) \sigma_{z}-i t^{\prime} \partial_{x} \sigma_{x} s_{z}$$

采用边界条件为$\psi_\alpha(0)=\psi_\alpha(\infty)=0$，求解本征方程$H_1\psi=E_\alpha\psi$，对于x=0处的零能解有两个

$$\psi_{\alpha}=\mathcal{N} \sin \left(\kappa_{1} x\right) e^{-\left(\kappa_{2} x\right)} e^{i k_{y} y} e^{i k_{z} z} \chi_{\alpha}$$

归一化系数$\mathcal{N}=2 \sqrt{\kappa_{2}\left(\kappa_{1}^{2}+\kappa_{2}^{2}\right) / \kappa_{1}^{2}}$

$$\kappa_{1}=\sqrt{\frac{-2 \tilde{m}-t k_{y}^{2}-t_{3} k_{z}^{2}}{t}-\left(\frac{t^{\prime}}{t}\right)^{2}}, \kappa_{2}=\frac{t^{\prime}}{t}$$

波函数还要满足$\sigma_{y} s_{z} \chi_{\alpha}=-\chi_{\alpha}$

## 满足条件的推导

由于$\psi_\alpha$是$H_1$的本征态，对应的本征值为0，则Pauli矩阵的作用对象就是$\chi_\alpha$

$$(\sigma_zs_0-i\sigma_xs_z)\chi_\alpha=0$$

最终目的就是要把括号中的表达式化简成一边是Pauli矩阵，另一边是常数，也就是本征方程的形式

$$\sigma_x\sigma_y=i\sigma_z,\sigma_i^2=1$$

利用上面Pauli矩阵的性质可以得到

$$-i\sigma_x\sigma_ys_0-i\sigma_xs_z=0$$

将两边的$-i\sigma_x$同时消去得到$\sigma_ys_0=-s_z$,然后在两边同时乘以$s_z$,则可以得到最终的结果

$$\sigma_ys_z=-1$$

> 在这里要说明一下，$\sigma_i,s_i$代表的是不同的自由度，$\sigma_xs_y$这种形式代表的是直积，$-i\sigma_x\sigma_y$是同一个自由度Pauli矩阵，它们在一起是代表矩阵的乘积，所以才有了上面在等式两端同时除以$-i\sigma_x$的。

