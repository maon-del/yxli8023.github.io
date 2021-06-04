---
title: 时间反演不变绝缘体的拓扑场论(.....ing)
tags: Topology
layout: article
license: true
toc: true
key: a20210604
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
这篇博客中,整理自己在学习拓扑绝缘体相关的拓扑场论过程中的一些概念整理和自己的笔记.
{:.info}
<!--more-->

第一Chern数:对Berry 位相规范场的曲率在整个BZ中的积分.

在1D时,在绝热演化的泵浦循环周期中,电子极化或者净电荷泵浦数目正好对应于Berry位相在动量及参数混合空间中的积分,和Chern数也存在一定的关联(2D).这个积分得到的整数正是量子化的拓扑数.

拓扑磁电效应(TME):外加一个电场,会在相同的方向上诱导出磁场,其比值是个普适的常数,一个奇数乘以乘以精细结构常数$\alpha=e^2/(\hbar c)$.

# 第一Chern数及(2+1)维拓扑响应函数

一个(2+1)维的紧束缚哈密顿量为

$$H=\sum_{m,n;\alpha,\beta}c^\dagger_{m\alpha}h^{\alpha\beta}_{mn}c_{n\beta}$$

在实空间中,矩阵的维度大小及对应着能带数目,$\alpha,\beta=1,2,\cdots,N$.当系统具有平移对称性的时候$h^{\alpha\beta}_{mn}=h^{\alpha\beta}(\vec{r}_m-\vec{r}_n)$哈密顿量可以在Bloch基矢下写成对角形式

$$H=\sum_{\bf k}c^\dagger_{\mathbf{k}\alpha}h^{\alpha\beta}({\bf k})c_{\mathbf{k}\beta}$$

当存在外部电磁场耦合时$h^{\alpha\beta}_{mn}\rightarrow h^{\alpha\beta}_{mn}e^{iA_{mn}}$,这里$A_{mn}$是订立在离散格点上的规范势.在线性阶近似下,耦合电磁场的哈密顿量为

$$H\simeq\sum_{\bf k}c^\dagger_{\bf k}h({\bf k})c_{\bf k}+\sum_{\bf k,q}A^i(-{\bf q})c^\dagger_{\bf k+q/2}\frac{\partial h({\bf k})}{\partial k_i}c_{\bf k-q/2}$$

系统对外场$A^i({\bf q})$的直流响应可以通过标准的Kubo公式得到

$$\sigma_{ij}=\text{lim}_{\omega\rightarrow 0}\frac{i}{\omega}Q_{ij}(\omega+i\delta),\quad Q_{ij}(i\nu_m)=\frac{1}{\Omega\beta}\sum_{\mathbf{k},n}\text{Tr}\{J_i({\bf k})G[\mathbf{k},i(\omega_n+\nu_m)]\cdot J_j(\mathbf{k})G(\mathbf{k},i\omega_n)\}\label{h4}$$

对于直流电$J_i({\bf k})=\frac{\partial h({\bf k})}{\partial k_i},i,j=x,y$,格林函数$G(\mathbf{k},i\omega_n)=[i\omega_n-h({\bf k})]^{-1}$,$\Omega$表示系统的表面积.当系统是个绝缘体的时候,$M$个占据态,c此时系统的纵向电导为零$\sigma_{xx}=0$,而横向电导为

$$\sigma_{xy}=\frac{e^2}{h}\frac{1}{2\pi}\int dk_x\int dk_yf_{xy}({\bf k}),\quad f_{xy}({\bf k})=\frac{\partial a_y({\bf k})}{\partial k_x}-\frac{\partial a_x({\bf k})}{\partial k_y},\\ a_i({\bf k})=-i\sum_{\alpha\in\text{occ}}\langle\alpha\mathbf{k}\rvert\frac{\partial}{\partial k_i}\rvert\alpha\mathbf{k}\rangle,\quad i=x,y$$$$

物理上$a_i({\bf k})$是动量空间中Berry位相规范场的$U(1)$分量.量子化的第一Chern数为

$$C_1=\frac{1}{2\pi}\int k_x\int k_y f_{xy}({\bf k})\in\mathbb{Z}$$

对于任意定义在BZ上的连续态$\rvert\alpha\mathbf{k}\rangle$都是满足的.由于电荷守恒,Hall效应响应为$j_i=\sigma_H\epsilon^{ij}E_j$同样会诱导出另外一个响应方程

$$j_i=\sigma_H\epsilon^{ij}E_j\rightarrow\frac{\partial\rho}{\partial t}=-\nabla\cdot{\bf j}=-\sigma_H\nabla\times \mathbf{E}=\sigma_H\frac{\partial B}{\partial t},\rightarrow\rho(B)-\rho_0=\sigma_HB\label{h1} $$

这里$\rho_0=\rho(B=0)$是基态的电荷密度.将(\ref{h1})结合磁轭城一个协变形式为

$$j^\mu=\frac{C_1}{2\pi}\epsilon^{\mu\nu\tau}\partial_\nu A_\tau\label{h2}$$

这里$\mu,\nu,\tau=0,1,2$分别是时间和空间索引.此时选择自然单位制$e=\hbar=1,e^2/h=1/2\pi$.

响应(\ref{h2})可以有外场$A_\mu$的Chern-Simons拓扑场论描述

$$S_\text{eff}=\frac{C_1}{4\pi}\int d^2x\int dt A_\mu\epsilon^{\mu\nu\tau}A_\tau$$

由$\delta S_\text{eff}/\delta A_\mu=j^\mu$既可以得到响应电流(\ref{h2}).这样的有效作用量是拓扑不变的,和第一Chern数的性质相同,所有量子霍尔态的拓扑响应都可以通过Chern-Simons理论来描述.

## Example:Two band models

考虑一个实际的两带模型

$$h({\bf k})=\sum_{a=1}^3[d_a({\bf k})\sigma_a+\epsilon({\bf k})\mathbb{1}]$$

这里$\mathbb{1}$是$2\times 2$的单位矩阵,$\sigma_a$是Pauli矩阵,这里$\sigma_a$可以表示自旋或者轨道,如果是真自旋则$\sigma_a$在时间反演操作下是增加一个负号的,如果$d_a({\bf k})$是奇函数,那么哈密顿量是满足时间反演不变的.如果任何一个$d_a$包含常数项,那么这个模型是破坏时间反演的.如果$\sigma_a$表示赝自旋(轨道),此时$\mathcal{T}^2=1$,只有$\sigma_y$在时间反演操作下出现一个负号,$\sigma_x,\sigma_z$都是不变的.单位矩阵在时间反演操作下是不变的,所以$\epsilon({\bf k})$在时间反演操作下是偶函数.上面哈密顿量对应的能谱为$E({\bf k})=\epsilon({\bf k})\pm\sqrt{\sum_ad^2_a({\bf k})}$.

在单粒子哈密顿量$h({\bf k})$中,矢量${\bf d(k)}$就像是作用在两能级赝自旋$\sigma_i$上的Zeeman场,占据态能带满足$[{\bf d(k)\cdot\sigma}]\rvert -,\mathbf{k}\rangle=-\rvert{\bf d(k)}\rvert\rvert-,\mathbf{k}\rangle$,这表明spinor的自旋极化方向为${\bf -d(k)}$,因此在$\rvert-,\mathbf{k}\rangle$上沿着某个${\bf k}$空间的路径$C$进行绝热演化时获得的Berry位相等于自旋$1/2$的粒子在磁场中沿着$\mathbf{d}(C)$绝热旋转时获得的Berry位相,**着正就是由路径$\mathbf{d}(C)$所张开的立体角的一半.**因此第一Chern数$C_1$可以被${\bf d(k)}$围绕原点的winding来确定

$$C_1=\frac{1}{2\pi}\int dk_x\int dk_y\hat{\bf d}\cdot\frac{\partial\hat{\bf d}}{\partial k_x}\times\frac{\partial\hat{\bf d}}{\partial k_y}$$

![png](tpf1.png)

一个实际的物理模型为

$h({\bf k})=\sin k_x\sigma_x+\sin k_y\sigma_y+(m+\cos k_x+\cos k_y)\sigma_z$

这里$\epsilon({\bf k})=0,{\bf d(k)}=(\sin k_x,\sin k_y,m+\cos k_x+\cos k_y)$,体系的Chern数为

$$C_1=\left\{\begin{array}{c}1\qquad\text{for $0<m<2$}\\-1\qquad\text{for $-2<m<0$}\\0\qquad\text{otherwise}\end{array}\right.$$

在$m\rightarrow 2$的连续极限下,模型可以约化为(2+1)-D的有质量Dirac哈密顿量

${\bf h(k)}=k_x\sigma_x+k_y\sigma_y+(m+2)\sigma_z=\left(\begin{array}{cc}m+2&k_x-ik_y\\ k_x+ik_y&-m-2\end{array}\right)$

在实空间中的紧束缚形式为

$$H=\sum_n[c^\dagger_n\frac{\sigma_z-i\sigma_x}{2}c_{n+\hat{x}}+c^\dagger_n\frac{\sigma_z-i\sigma_y}{2}c_{n+\hat{y}}+\text{H.c}]+m\sum_nc^\dagger_n\sigma_zc_n\label{h3}$$

这个模型可以描述量子反常霍尔效应,体系统是存在自旋轨道耦合($\sigma_x,\sigma_y$)以及铁磁极化$\sigma_z$.

## 维度约化

为了研究第一Chern数和拓扑响应之间的联系,可以通过维度约化来进行,首先在一个圆柱结构上研究量子霍尔态.一个非平庸的量子霍尔系统会存在手性边界态,对于最简单的Chern数$C_1=1$的情况,系统每个边界上都会存在一支手性费米子.可以将哈密顿量(\ref{h3})放在一个圆柱体结构上进行计算(一个方向是周期边界,另外一个方向是开边界).此时周期边界方向的的$k$是一个好量子数,进行一个部分Fourier变换

$c_{k_ya}(x)=\frac{1}{\sqrt{L_y}}\sum_yc_\alpha(x,y)e^{ik_yy}$

这里的$(x,y)$表示正方点整上的坐标,最后可以将哈密顿量(\ref{h3})改写为

$H=\sum_{k_y,x}[c^\dagger_{k_y}(x)\frac{\sigma_z-i\sigma_x}{2}c_{k_y}(x+1)+\text{H.c}]+\sum_{k_y,x}c^\dagger_{k_y}(x)[\sin k_y\sigma_y+(m+\cos k_y)\sigma_z]c_{k_y}(x)\equiv\sum_{k_y}H_\text{1D}(k_y)$

在经过这个变换之后就可以将原本的2D系统看做是一个$L_y$依赖的1D紧束缚模型链,$L_y$表示在$y$方向上的周期晶格数目.而哈密顿量$H_\text{1D}$的本征值可以在每个$k_y$下通过数值方式求解,如下图所示

![png](tpf2.png)

可以发现此时有个很明显的边界态会穿过体能隙,并且分别位于$x=0,L_x$这两个边界上.而且每条边界态的手性(费米速度)也是不同的,从图中也可以看出费米速度$v=\partial E/\partial k$对于左边界态总是正的,而对于右边界态总是负的,霍尔效应可以通过Laughlin的规范讨论来进行理解.考虑一个沿着$y$方向的电场$E_y$,可以表示为

$A_y=-E_yt,\quad A_x=0$

将哈密顿量改写为$H=\sum_kH_\text{1D}(k_y+A_y)$,沿着$x$方向的电流为

$J_x=\sum_{k_y}J_x(k_y)$

$J_x(k_y)$是一维系统的电流,此时2D系统的Hall响应可以通过参数化的1D系统$H_\text{1D}$决定,含时变化为$q(t)-k_y+A_y(t)$.规范势$A_y$对应着一个通量$\Phi=A_yL_y$穿过整个圆柱体结构,在一个周期变化中$0\leq t\leq2\pi/L_yE_y$通量从$0$变化到$2\pi$,而这个过程中流过系统的电荷为

$\Delta Q=\int_0^{\Delta t}dt\sum_{k_y}J_x(k_y)\equiv\sum_{k_y}\Delta P_x(k_y)\rvert_0^{\Delta t}$

一个周期中$\Delta t=2\pi/L_yE_y$,在第二个恒等式中利用了1D系统中电荷极化与电流的关系$T_x(k_y)=dP_x(k_y)/dt$,在热力学极限下系统总是处在$H_{1D}[q(t)]$的基态中,因此极化的改变$\Delta P_x(k_y)=P_x(k_y-2\pi/L_y)-P_x(k_y)$.当$L_y\rightarrow\infty$时,$\Delta Q$表示为

$$\Delta Q=-\int_0^{2\pi}dk_y\frac{\partial p_x(k_y)}{\partial k_y}$$

穿过圆柱体结构的通量变化导致的Hall效应所产生的的电荷流动等于在一维系统$H_{1D}(k_y)$当$k_y$从0变化到$2\pi$时的电荷流动.从Hall响应可以得到$\Delta Q=\sigma_H\Delta tE_yL_y=2\pi\sigma_H$是个量子化的整数,可以从1D的图像上进行理解.当$k_y$在0到$2\pi$进行变化的时候,边界态的能量和位置将会发生变化,如上图所示.**由于在左(右)边界态的能量总是增加(减少)随着$k_y$的变化,在一个半填充的系统中电荷总会被泵浦到左边界,这将会使得$\Delta Q=-1$**.这个量子化的值可以通过计算极化$P_x(k_y)$来得到,如上图(d)所示,当$P_x$在一边发生一个跃变的时候,就会有$\Delta Q=-1$.

上面维度约化的研究可以适用于任何一个2D的绝缘体系统,对于一般的2D系统可以定义其对应的1D系统为

$$H_{1D}(\theta)=\sum_{k_x}c^\dagger_{k_x,\theta}h(k_x,\theta)c_{k_x,\theta}$$

此时用$\theta$代替了有方向的动量$k_y$,并且替代了$q(t)$,当$\theta$是含时的,可以通过Kubo公式(\ref{h4})来计算电流响应,只不过此时对$(k_x,k_y)$的求和变成了只对$k_x$进行求和.线性响应可以定义为

$$J_x(\theta)=G(\theta)\frac{d\theta}{dt},\quad G(\theta)=\text{lim}_{\omega\rightarrow 0}\frac{i}{\omega}Q(\omega+i\delta;\theta)\\ Q(i\omega_n;\theta)=-\sum_{k_x,i\nu_m}\text{Tr}\{J_x(k_x;\theta)G_{1D}[k_x,i(\nu_m+\omega_n);\theta]\times\frac{\partial h(k_x;\theta)}{\partial \theta}G_{1D}(k_x,i\omega_n;\theta\}\frac{1}{L_x\beta}\label{h5}$$

响应系数格局Berry位相规范场表示为

$$G(\theta)=-\int\frac{dk_x}{2\pi}f_{x\theta}(k_x,\theta)=\int\frac{dk_x}{2\pi}(\frac{\partial a_x}{\partial \theta}-\frac{\partial a_\theta}{\partial k_x}),\quad \int G(\theta)d\theta=C_1\in\mathbb{Z}$$

如果选择一个合适的规范,使得$a_\theta$总是单只的,则$G(\theta)$可以进一步简化

$G(\theta)=\frac{\partial}{\partial \theta}(\int\frac{dk_x}{2\pi}a_x(k_x,\theta))\equiv\frac{\partial P(\theta)}{\partial \theta},\quad P(\theta)=\int dk_xa_x/2\pi$

这正是1D系统对应的电荷极化,响应函数变为$J_x=\partial P/\partial t$.**因为电子极化P的定义是电子的质心位置偏移格点的大小,所以它的定义只有mod 1才是well defined**.因此一个周期演化的变化量$\Delta P=P(\theta=2\pi)-P(\theta=0)$是个整数,等于$-C_1$,也正好对应着整个系统的电荷泵浦数目.
{:.success}

和量子Hall情况相似,电流响应将会导致电荷密度的响应,着可以通过电荷守恒条件来确定,当参数$\theta$同时具有时间和空间变化时$\theta(x,t)$,响应方程(\ref{h5})仍然适用,从连续性方程可得到

$$\frac{\partial\rho}{\partial t}=-\frac{\partial J_x}{\partial x}=-\frac{\partial^2P(\theta)}{\partial x\partial t}\rightarrow\rho=-\frac{\partial P(\theta)}{\partial x}$$

这里电荷密度$\rho$是基于背景电荷而言.此时密度与电流响应可以写为

$$j_\mu=-\epsilon_{\mu\nu}\frac{\partial[\theta(x,t)]}{\partial x_\nu},\quad\mu,\nu=0,1\text{分别是时间和空间}$$

一般情况下当哈密顿量随着时间和空间是平缓变时,单粒子哈密顿量$h(k)$变为$h(k,x,t)=h[k,\theta(x,t)]$,其对应的本征态为$\rvert\alpha;k,x,t\rangle$,这里的$\alpha$是能带索引.定义在相空间中的Berry位相规范场

$\mathcal{A}_A=-i\sum_\alpha\langle\alpha;q_A\rvert\frac{\partial}{\partial q_A}\rvert\alpha;q_A\rangle,\quad\mathcal{F}_{AB}=\partial_A\mathcal{A}_B-\partial_B\mathcal{A}_A$

相空间流为

$$j^p_A=-\frac{1}{4\pi}\epsilon_{ABC}\mathcal{F}_{BC}$$

实际的物理流可以通过对波矢流型进行积分得到

$j_\mu=\int dkj^P_\mu=-\int\frac{dk}{2\pi}\epsilon^{\mu2\nu}\mathcal{F}_{2\nu},\quad\mu,\nu=0,1$

对于一个SSH模型

$$h(k,\theta)=\sin k\sigma_x+(\cos k-1)\sigma_z+m(\sin\theta\sigma_y+\cos\theta\sigma_z),\quad m>0$$

在$m<<1$的极限下,将哈密顿量展开成连续模型$h(k,\theta)\simeq k\sigma_x+m(\sin\theta\sigma_y+\cos\theta\sigma_z)$,着是一个连续的(1+1)D Dirac模型,有一个实质量$m\cos\theta$和一个虚质量$m\sin\theta$,根据前面的讨论,此时极化$\int dk_xa_x/2$可以由矢量$\mathbf{d}(k)=(\sin k,m\sin\theta,m\cos\theta+\cos k-1)$所张开的立体角来决定,如下图所示

![png](tpf3.png)

在$m<<1$的即现在,可以发现张开的立体角$\Omega(\theta)=2\pi$,因此极化$P(\theta)\simeq\theta/2\pi$,响应电流为

$$j_\mu=-\epsilon_{\mu\nu}\partial_\nu\theta$$

在$\theta$场的畴壁上电荷积累为$Q=\int_{-\infty}^{+\infty}(d\theta/dx)(dx/2\pi)=-[\theta(+\infty)-\theta(-\infty)]/2\pi$.对于反位相的畴壁$\theta(+\infty)-\theta(-\infty)=\pi$,从而可以得到此时的存在分数电荷$q=\frac{1}{2}$.

## (1+1)维$\mathbb{Z}_2$分类粒子空穴对称绝缘体
对于一个一维的紧束缚哈密顿量$H=\sum_{mn}c^\dagger_{m\alpha}h^{\alpha\beta}_{mn}c_{n\beta}$粒子空穴变换定义为$c_{m\alpha}\rightarrow C^{\alpha\beta}c^\dagger_{m\beta}$,这里电荷共轭矩阵$C$满足$C^\dagger C=\mathbb{I},C^*C=\mathbb{I}$.在周期性边界条件下对称性要求

$$H=\sum_kc^\dagger_kh(k)c_k=\sum_kc_{-k}C^\dagger h(k)Cc^\dagger_{-k}\rightarrow C^\dagger h(-k)C=-h^T(k)$$

从上式可以知道,如果$E$是$h(0)$的本征值,那么$-E$也是,即哈密顿量的能谱是正负对称的.如果$h(k)$的维度是奇数,那么至少存在一个零能本征值$E=0$.此时因为$h$是traceless 的,因此化学势为零,这个系统不能被打开能隙,除非$h$的维度是偶数.

现在考虑两个满足粒子空穴对称的绝缘体哈密顿量$h_1(k),h_2(k)$.通常可以在两者之间插入一个连续的$h(k,\theta)$其定义为

$$h(k,0)=h_1(k),\quad h(k,\pi)=h_2(k)$$

而且总是可以找到一个合适的参数使得$\theta\in[0,\pi]$区间内$h(k,\theta)$总是有能隙的.总而言之,拓扑空间中所有1D拓扑绝缘体$h(k,\theta)$都是相互联系的,这也是**Neumann–Wigner theorem  **保证的.

假设$h(k,\theta)$是在$h_1(k),h_2(k)$之间一个有能隙的,通常在$\theta\in[0,\pi],h(k,\theta)$不必要满足粒子空穴对称,对$\theta\in[\pi,2\pi]$定义

$$h(k,\theta)=-[C^{-1}h(-k,2\pi-\theta)C]^T\label{ha6}$$

选择这个参数化视为了当$\theta$被替换为高位空间中的动量波矢的时,哈密顿量满足粒子空穴对称.由于$h(k,\theta=0)$与$h(k,\theta=\pi)$的例子空穴对称,在$\theta\in[0,2\pi]$区间内$h(k,\theta)$是连续的,且$h(k,2\pi)=h(k,0)$.当$\theta$从0到$2\pi$进行绝热演化并对$h(k,\theta)$定义一个周期绝热泵浦,此时第一Chern数是定义在$(k,\theta)$空间中的,Chern数$C[h(k,\theta)]$可以表示成极化的winding number

$$C[h(k,\theta)]=\int d\theta\frac{\partial p(\theta)}{\partial\theta},\quad p(\theta)=\int\frac{dk}{2\pi}\sum_{E_\alpha(k)<0}(-i)\langle k,\theta;\alpha\rvert\partial_k\rvert k,\theta;\alpha\rangle$$

这里求和是对所有的占据态进行的.通常情况下两个不同的参数化$h(k,\theta),h^{'}(k,\theta)$会对应着不同的Chern数$C[h(k,\theta)]\neq C[h^{'}(k,\theta)]$,然而由对称限制(\ref{ha6})保证这两个不同的Chern数相差偶数$C[h(k,\theta)]-C[h^{'}(k,\theta)]=2n,n\in\mathbb{Z}$.


















# 参考

- 1.[Topological field theory of time-reversal invariant insulators](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.78.195424)
