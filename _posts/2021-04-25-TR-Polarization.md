---
title: 时间反演极化
tags: topology
layout: article
license: true
toc: true
key: a20210425b
pageview: true
aside:
    toc: true
sitemap: true
mathjax: true
author: YuXuan
show_author_profile: true
---
满足时间反演不变的体系, Chern数为0, 但是可以通过$Z_2$拓扑不变量描述, 任然可以通过一个物理图像来理解这个不变量和某一种极化之间的对应关系, 这里整理一下时间反演极化与$Z_2$拓扑不变量之间的联系.
<!--more-->

虽然存在时间反演不变时, Berry曲率是个奇函数, 对BZ的积分为0, 但是任然可以通过$Z_2$拓扑不变量进行描述, 这里主要整理一下如何通过时间反演极化, 将一个具体的物理图像和$Z_2$拓扑不变量联系起来.
{:.info}

考虑一个1D能带结构, 它是具有$\frac{1}{2}$自旋满足时间反演对称的系统, 此时可以不用在考察整个BZ, 而只需要考虑半个BZ即可, 另外一半可以通过时间反演联系起来. 体系存在时间反演对称性时, 能带总是成对出现的, 系统整体的性质可以通过只考虑布里渊区中Kramers对中的一支即可.

时间反演对称将$k$的能带$\alpha$变换到$-k$的能带$\beta$,这里的$\alpha,\beta$是Kramers对,它们之间会相差一个位相因子

$$\rvert u^\alpha_{-k,a}\rangle=e^{i\chi_{k,a}}T\rvert u^\beta_{k,a}\rangle\label{2}$$

时间反演操作算符$T$作用后

$$T\rvert u^\alpha_{-k,a}\rangle=Te^{i\chi_{k,a}}T\rvert u^\beta_{k,a}\rangle=e^{-i\chi_{k,a}}T^2\rvert u^\beta_{k,a}\rangle=-e^{-i\chi_{k,a}}\rvert u^\beta_{k,a}\rangle$$

所以可以得到

$$\rvert u^\beta_{-k,a}\rangle=-e^{-i\chi_{-k,a}}T\rvert u^\alpha_{k,a}\rangle$$

从上面可以看出, 在$\rvert u_{k,n}\rangle=\sum_mU_{mn}\rvert u_{k,m}\rangle$变换下它们并不是规范不变的表示,为了计算的目的, 将要找到一个规范不变的表示进行计算. 首先对时间反演不变Kramers对中的每一支来计算计算极化

$$P^s=\frac{1}{2\pi}\int_{-\pi}^{\pi}dkA^s(k)\qquad A^s(k)=i\sum_a\langle u^s_{k,a}\rvert\nabla_k\rvert u^s_{k,a}\rangle\qquad s=\alpha,\beta$$

接下来将两支的极化联系起来

$$P^\alpha=\frac{1}{2\pi}\int_0^{\pi}(A^\alpha(k)+A^\alpha(-k))$$

利用时间反演算符(\ref{2})可以得到

$$\begin{aligned}A^\alpha(-k)&=-i\sum_a\langle u^\alpha_{-k,a}\rvert\nabla_k\rvert u^\alpha_{-k,a}\rangle\\&=-i\sum_a\langle Tu^\beta_{k,a}\rvert\nabla_k\rvert Tu^\beta_{k,a}\rangle-i\sum_ai\nabla_k\chi_{k,a}\langle Tu^\beta_{k,a}\rvert Tu^\beta_{k,a}\rangle\\&=-i\sum_a\langle Tu^\beta_{k,a}\rvert\nabla_k\rvert Tu^\beta_{k,a}\rangle-i\sum_ai\nabla_k\chi_{k,a}\end{aligned}$$

$$\begin{aligned}\langle Tu^\beta_{k,a}\rvert\nabla_k\rvert Tu^\beta_{k,a}\rangle&=(U_{mn}u^{\beta*}_{k,a,n})^{*}\nabla_k U_{mp}u^{\beta *}_{k,a,p}=(U^\dagger)_{mn}U_{mp}u^\beta_{k,a,n}\nabla_ku^{\beta *}_{k,a,p}\\&=u^\beta_{k,a,n}\nabla_ku^{\beta *}_{k,a,n}=-u^{\beta *}_{k,a,n}\nabla_k u^{\beta}_{k,a,n}=-\langle u^\beta_{k,a}\rvert\nabla_k\rvert u^\beta_{k,a}\rangle\end{aligned}$$

综上可以得到

$$A^\alpha(-k)=i\sum_a\langle u^\beta_{k,a}\rvert\nabla_k\rvert u^\beta_{k,a}\rangle+\sum_a\nabla_k\chi_{k,a}=A^\beta(k)+\sum_a\nabla_k\chi_{k,a}$$

可以得到极化为

$$\begin{aligned}P^\alpha&=\frac{1}{2\pi}(\int_0^\pi(A^\alpha(k)+A^\beta(k))+\int_0^\pi\sum_a\nabla_k\chi_{k,a})\\&=\frac{1}{2\pi}(\int_0^\pi A(k)+\sum_a(\chi_{\pi,a}-\chi_{0,a}))\end{aligned}\qquad A(k)=A^\alpha(k)+A^\beta(k)\label{eq2}$$

最后一项可以通过$U(2N)$的sewing matrix进行改写

$$B_{mn}=\langle u_{-k,m}\rvert T\rvert u_{k,n}\rangle$$

这里$\rvert u_{\pm k,m}\rangle$代表的是所有的占据态,利用关系式

$$\rvert u^\alpha_{-k,a}=e^{i\chi_{k,a}}T\rvert u^\beta_{k,a}\rangle,\rvert u^\beta_{-k,a}\rangle=-e^{i\chi_{-k,a}}T\rvert u^\alpha_{k,a}\rangle$$

得到

$$B^{\beta,\alpha}_{mn}(k)=\langle u^\beta_{-k,m}\rvert T\rvert u^\alpha_{k,n}\rangle=-\delta_{mn}e^{-i\chi_{-k,n}},B^{\alpha,\beta}_{mn}=-B^{\beta,\alpha}_{mn}(-k)$$

$B^{\beta,\alpha}_{mn}$是Kramers对能带$\alpha,\beta$的sewing matrix,这里可以存在多个Kramers对$m=1,2,\cdots,N$, 但是sewing matrix 耦合Kramers对是两两组合的, 所以矩阵$B$将会变成分块非对角形式

$$B=\left[\begin{array}{cc}0&-e^{-i\chi_{-k,n}}\\e^{-i\chi_{k,n}}&0\end{array}\right]$$

可以看到在$k=0,\pi$处, 矩阵$B$是反对称的, 故而可以将(\ref{eq2})中的第二项改写为

$$\sum_a(\chi_{\pi,a}-\chi_{0,a})=i\text{log}\left[\frac{\text{Pf}[B(\pi)]}{\text{Pf}[B(0)]}\right]$$

对于能带$\alpha$的极化

$$P^\alpha=\frac{1}{2\pi}(\int_0^\pi dk A(k)+i\text{log}\left[\frac{\text{Pf}[B(\pi)]}{\text{Pf}[B(0)]}\right])$$

将能带$\alpha,\beta$的极化叠加起来, 就可以得到整体的极化

$$P=\frac{1}{2\pi}\int_{-\pi}^\pi dk A(k)=P^\alpha+P^\beta$$


