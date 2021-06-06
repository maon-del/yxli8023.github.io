---
title: 时间反演不变绝缘体的拓扑场论(.....ing)
tags: Topology Field-Theory
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

$$C_1=\frac{1}{2\pi}\int dk_x\int dk_y\hat{\bf d}\cdot\frac{\partial\hat{\bf d}}{\partial k_x}\times\frac{\partial\hat{\bf d}}{\partial k_y}\label{c1}$$

![png](/assets/images/topology/tpf1.png)

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

![png](/assets/images/topology/tpf2.png)

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

$$\frac{\partial\rho}{\partial t}=-\frac{\partial J_x}{\partial x}=-\frac{\partial^2P(\theta)}{\partial x\partial t}\rightarrow\rho=-\frac{\partial P(\theta)}{\partial x}\label{ha8}$$

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

![png](/assets/images/topology/tpf3.png)

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

接下来证明上面的结论,对$h(k,\theta)$的本征态$\rvert k,\theta;\alpha\rangle$对应的本征值$E_\alpha(k,\theta)$,利用(\ref{ha6})可得

$$h(-k,2\pi-\theta)C\rvert k,\theta;\alpha\rangle^*=-E_\alpha(k)C\rvert k,\theta;\alpha\rangle^*$$

$\rvert k,\theta;\alpha\rangle^*=\sum_\beta(\langle m,\beta\rvert k,\theta;\alpha\rangle^*)\rvert m,\beta\rangle,$这里$m,\beta$分别是未知空间格点和轨道索引.因此$C\rvert k,\theta;\alpha\rangle^*\equiv\rvert -k,2\pi-\theta;\bar{\alpha}\rangle$是$h(-k,2\pi-\theta)$的本征态,对应的本征值为$E_{\bar{\alpha}}(k,2\pi-\theta)=-E_\alpha(k,\theta)$.哈密顿量$h(k,\theta)$与$h(-k,2\pi-\theta)$的本征态是一一对应的,从而可以得到

$$P(\theta)=\int\frac{dk}{2\pi}\sum_{E_\alpha(k)<0}(-i)\langle k,\theta;\alpha\rvert\partial_k\rvert k,\theta;\alpha\rangle=\int\frac{dk}{2\pi}\sum_{E_{\bar{\alpha}(-k)}>0}(-i)(\langle -k,2\pi-\theta;\bar{\alpha}\rvert)^*\cdot\partial_k\rvert -k,2\pi-\theta;\bar{\alpha}\rangle^*=-P(2\pi-\theta)\label{ha7}$$

因此$P(\theta)\quad\text{mod}\quad1$是well defined,(\ref{ha7})表明$P(\theta)+P(2\pi-\theta)=0\quad\text{mod}\quad 1$.对于$\theta=0$或者$\theta=\pi$有$2\pi-\theta=0\quad\text{mod}\quad 2\pi$,从而得到$P(\theta)=0\quad or\quad1/2$.也就是说极化取值为$1$或者$1/2$对任何满足粒子空穴对称的绝缘体.**如果两个系统具有不同的极化P,在不破坏粒子空穴对称情况下,是不能通过绝热演化相互转换的,因为在绝热演化过程中P是个连续函数,当它不是0或者1/2时就破坏了粒子空穴对称.**这也就解释了为什么在存在粒子空穴对称的情况下系统是$\mathbb{Z}_2$分类的.有前面的定义可知极化$P(\theta)=\int dk a_k/2\pi$是规范依赖的,下面就来定义一个更加普遍的$\mathbb{Z}_2$表达式,它仅包含规范不变量$\partial P(\theta)/\partial\theta$和Chern数$C_1$.

由对称性(\ref{ha7})可得

$$\int_0^\pi dP(\theta)=\int_\pi^{2\pi}dP(\theta)\label{ha8}$$

它是规范独立的,因为只包含了极化$P(\theta)$的变化.这个方程表明在闭合路径的前半部分与后半部分极化的变化都是相同的.考虑两个不同的参数化过程$h(k,\theta),h^{'}(k,\theta)$满足$h(k,0)=h^{'}(k,0)=h_1(k),h(k,\pi)=h^{'}(k,\pi)=h_2(k)$.这里$h(k,\theta),h^{'}(k,\theta)$对应的极化分别为$P(\theta),P^{'}(\theta)$,二者对应的Chern数之差为

$$C[h]-C[h^{'}]=\int_0^{2\pi}d\theta(\frac{\partial P(\theta)}{\partial\theta}-\frac{\partial P^{'}(\theta)}{\partial\theta})$$

定义新的差值$g_1(k,\theta),g_2(k,\theta)$

$$g_1(k,\theta)=\left\{\begin{array}{c}h(k,\theta),\quad\theta\in[0,\pi]\\h^{'}(k,2\pi-\theta),\quad\theta\in[\pi,2\pi]\end{array}\right.\\g_2(k,\theta)=\left\{\begin{array}{c}h^{'}(k,2\pi-\theta),\quad\theta\in[0,\pi]\\h(k,\theta),\quad\theta\in[\pi,2\pi]\end{array}\right.$$

这里$g_1(k,\theta)$与$g_2(k,\theta)$只是重新组合对两个路劲$h(k,\theta),h^{'}(k,\theta)$进行了组合,如下图所示

![png](/assets/images/topology/tpf4.png)

从$g_1,g_2$的构建路径可以直接得到

$C[g_1]=\int_0^\pi d\theta(\frac{\partial P(\theta)}{\partial \theta}-\frac{\partial P^{'}(\theta)}{\partial\theta})\\ C[g_2]=\int^{2\pi}_\pi d\theta(\frac{\partial P(\theta)}{\partial\theta}-\frac{\partial P^{'}(\theta)}{\partial\theta})$

因此可以得到$C[h]-C[h^{'}]=C[g_1]+C[g_2]$,由(\ref{ha8})可以得到$C[g_1]=C[g_2]$,从而$C[h]-C[h^{'}]=2C[g_1]$.由于$C[g_1]\in\mathbb{Z}$我们可以得到$C[h]-C[h^{'}]$的取值是偶数.Chern数$C[h],C[h^{'}]$的不同是因为它们对应的路径之间存在奇异点,而且由于粒子空穴对称性的存在,这个奇异点的位置也是对称的.基于上面的讨论,可以定义一个相对Chern宇称

$$N_1[h_1(k),h_2(k)]=(-1)^{C[h(k,\theta)]}$$

它与$h(k,\theta)$的选取无关,只决定于哈密顿量$h_1(k),h_2(k)$.而且对于任意三个粒子空穴对称的哈密顿量$h_1(k),h_2(k),h_3(k)$总是满足

$N_1[h_1(k),h_2(k)]N_1[h_2(k),h_3(k)]=N_1[h_1(k),h_3(k)]$

由$N_1[h_1(k),h_2(k)]=1$在任意两个粒子空穴对称哈密顿量之间定义了一个等价关系,因此可以将所有满足粒子空穴对称的哈密顿量分成两类.定义一个真空态$h_0(k)\equiv h_0$,这里$h_0$是任意一个不依赖于动量$k$的矩阵且满足粒子空穴对称$C^\dagger h_0C=-h_0^T$,可以认为$h_0$描述的是一个没有hopping完全局域的系统,将它作为一个平庸的参考态可以得到$N_1[h_0(k),h_1(k)]\equiv N_1[h(k)]$作为哈密顿量$h(k)$的$\mathbb{Z}_2$拓扑不变量.所有满足$N_1[h_0(k),h(k)]=1$的哈密顿量$h(k)$都是$\mathbb{Z}_2$平庸的,满足$N_1[h_0(k),h(k)]=-1$的都是$\mathbb{Z}_2$非平庸的.

对于一个$\mathbb{Z}_2$非平庸的哈密顿量$h_1(k)$可以定义一个差值$h(k,\theta)$满足$h(k,0)=h_0,h(k,\pi)=h_1(k)$,对应的Chern数为$C[h(k,\theta)]$为奇整数,如果研究一个一维开边界的系统$h(k,\theta)$,实空间中的紧束缚哈密顿量为

$$h_{mn}(\theta)=\frac{1}{\sqrt{L}}\sum_ke^{ik(x_m-x_n)}h(k,\theta),\quad 1\leq m,n\leq L$$

此时再$h(k,\theta)$的能隙中有一个束缚态,与非零的Chern数相关联.当Chern数$C[h(k,\theta)]=2n-1,n\in\mathbb{Z}$这里由一些值$\theta^L_s\in[0,2\pi),s=1,2,\cdots,2n-1$,此时哈密顿量$h_{mn}(\theta_s)$有零能的局域态在系统的左边界上,同样的有相同数目的零能态在有边界上其$\theta^R_s$与左端相同.

![png](/assets/images/topology/tpf5.png)

由于再$h_{mn}(\theta)$与$h_{mn}(2\pi-\theta)$之间有粒子空穴对称性的存在,零能态总是成对出现在$\theta$与$2\pi-\theta$处.当Chern数是奇数是,一定有零能级出现在$\theta=0$和$\theta=\pi$.由于$\theta=0$是个平庸的绝缘体,对应着平带因此不存在终端态,局域的零能拓扑态出现在$\theta=\pi$处.总而言之,一个粒子空穴对称的$\mathbb{Z}_2$拓扑绝缘体在开边界的时候会存在一个零能的局域态.存在零能级会有一个重要的物理结果，在非平庸拓扑绝缘体边界上将会存在半整数的电荷，在周期系统中当化学势为零的时候，当有$N$条占据的能带时，每个格点上平均的粒子数密度为$\bar{n}_m=\langle\sum_\alpha c^\dagger_{m\alpha}c_{m\alpha}\rangle=N$，在开放边界时相对于$N$的粒子数为$\rho_m(\mu)=\langle\sum_\alpha c^\dagger_{m\alpha}c_{m\alpha}\rangle_\mu-N$，粒子空穴对称性会保证$\rho_m(\mu)=-\rho_m(-\mu)$，当化学势$\mu$在能隙中间时，$\mu,-\mu$的区别就是零能态束缚在$\rvert 0L\rangle$还是$\rvert 0R\rangle$，对格点$m$足够远离右边界的时候

$$\text{lim}_{\mu\rightarrow 0^{+}}[\rho_m(\mu)-\rho_m(-\mu)]=\sum_\alpha\rvert\langle m\alpha\rvert 0L\rangle\rvert^2$$

当对左边界进行求和$\sum_m\rho_m(\mu\rightarrow 0^+)=1/2$，此时并不会包括另外一端的贡献。当零能态未被占据时边界上将会局域$1/2$个电子，当被占据时则会有$-1/2$个电子占据。从在半整数电荷也可以在开边界条件下，从非平庸于平庸相的质量畴壁视角来理解，通过对$h_{mn}(\theta)$定义插值，与空间依赖的畴壁为$\theta(x\rightarrow+\infty)=\pi,\theta(x\rightarrow-\infty)=0$，由相应公式(\ref{ha8})可得畴壁上积累的电荷为

$$Q_d=e\int_{-\infty}^{+\infty}dx\frac{\partial P[\theta(x)]}{\partial x}=e\int dP(\theta)=\frac{e}{2}\int_0^{2\pi}dP(\theta)=\frac{e}{2}C[h(k,\theta)]$$

这里需要强调，对于一个占据的局域态，其上面的电子总是可以变化整数个，也就是说$Q_d$只有$\text{mod}\quad e$才是有意义的，边界上存在分数的电荷$a\pm e/2$也仅仅在系统时拓扑非平庸的时候才满足。

## (0+1)维$\mathbb{Z}_2$分类粒子空穴对称绝缘体

对$(1+1)$维的系统进行围堵约化来研究$(0+1)$维系统的性质，这个维度约化的研究可以帮助理解后面$(2+1)$维时间反演不变(TRI)拓扑绝缘体从$(4+1)$维约化而来的过程。

自由粒子哈密顿量$h$满足粒子空穴对称表现为

$$C^\dagger hC=-h^T$$

给定两个满足粒子空穴对称的额哈密顿量$h_1,h_2$，利用和前面相同的处理过程在区间$\theta\in[0,2\pi]$定义连续插值$h(\theta)$满足

$$h(0)=h_1,\quad h(\pi)=h_2,\quad C^\dagger h(\theta)C=-h(2\pi-\theta)^T\label{ha9}$$

对所有的$\theta$而言$h(\theta)$都是有能隙的，哈密顿量$h(\theta)$是$(1+1)$维哈密顿量$h(k)$进行维度约化后的结果，此时波矢$k$被$\theta$代替。限制条件(\ref{ha9})正是粒子空穴对称性，所以$h(\theta)$就对应着满足粒子空穴对称的$(1+1)$维绝缘体，可以通过Chern宇称$N_1[h(\theta)]$来进行分类。如果$N_1[h(\theta)]=-1$，在哈密顿量$h(\theta)$与真空哈密顿量$h(\theta)=h_0,\theta\in[0,2\pi]$之间没有满足粒子空穴对称的连续插值存在。在$h_1,h_2$之间考虑两个不同的插值$h(\theta),h^{'}(\theta)$，通过结合律$N_1[h(\theta)]N_1[h^{'}(\theta)]=N_1[h(\theta),h^{'}(\theta)]$，它是两个插值路径的相对Chern宇称。因为$N_1[h(\theta)]$与$h_1,h_2$之间的插值是不相关的，所以$N_0[h_1,h_2]\equiv N_1[h(\theta)]$可以被定义为$h_1,h_2$的函数。此时$(0+1)维\mathbb{Z}_2$量$N_0$与$(1+1)$维时候的$N_1[h(k),h^{'}(\theta)]$扮演者相同的角色。

在$h(\theta),h^{'}(\theta)$之间定义连续插值$g(\theta,\varphi)$，它满足

$$g(\theta,\varphi=0)=h(\theta),\quad g(\theta,\varphi=\pi),h^{'}(\theta),\quad g(0,\varphi)=h_1,\quad g(\pi,\varphi)=h_2,\quad C^\dagger g(\theta,\varphi)C=-g(2\pi-\theta,2\pi-\varphi)^T$$

根据上一节的讨论可以简单的得到这样的连续插值总是可以存在的，对于所有的$\theta,\varphi$，函数$g(\theta,\varphi)$都是有能隙的。在两维参数空间$(\theta,\varphi)$中总是可以定义Berry位相和第一Chern数$C_1[g(\theta,\varphi)]$。通过定义Chern宇称可以得到$N_1[h(\theta),h^{'}(\theta)]=(-1)^{C_1[g(\theta,\varphi)]}$。参数化的哈密顿量可以从两个视角来看：不仅在$h(\theta),h^{'}(\theta)$间定义了插值，同样在$g(0,\varphi)=h_1,g(\pi,\varphi)=h_2$之间也定义了插值。无论$\varphi$去任何值，$g(0,\varphi),g(\pi,\varphi)$都是真空态哈密顿量，它们都有相对平庸的Chern宇称$N_1[h(\theta),h^{'}(\theta)]=N_1[g(0,\varphi),g(\pi,\varphi)]=N_1[h_1,h_2]=1$。

从上面的分析可以得到,任何两个属于相同$\mathbb{Z}_2$类的$h(\theta)$与$h^{'}(\theta)$,他们的Chern宇称$N_1[h(\theta)]$仅仅依赖于终点的$h_1,h_2$.也就是说$N_0[h_1,h_2]\equiv N_1[h(\theta)]$定义了一对粒子空穴对称哈密顿量$h_1,h_2$之间的关系.之后选择任意一个参考哈密顿量$h_0$,总是可以定义所有哈密顿量满足$N_0[h_0,h]=1$是平庸的$N_0[h_0,h]=-1$是非平庸的.此时与$(1+1)$维情况有所不同的是参考哈密顿量$h_0$的选择不是自然的.总而言之,平庸与非平庸仅仅在$(0+1)$维具有意义.但是分类仍然是有意义的,任意两个哈密顿量满足$N_0[h_1,h_2]=-1$都不能在不破坏粒子空穴对称的情况下绝热转换.**单格点粒子空穴对称哈密顿量的流形是不连通的,起码会存在两个连接的片段.**
{:.success}

考虑一个简单的$2\times 2$哈密顿量,通常单格点哈密顿量可以分解为

$$h=d_0\sigma^0+\sum_{a=1}^3d_a\sigma^a$$

当粒子空穴变换$C=\sigma^1$要求$C^\dagger hC=-h^T$时,从上面的表达式可以得到$d_0=d_1=d_2=0$,因此$h =d_3\sigma^3$,只要$d_3\neq 0$哈密顿量$h$就有能隙.下面来看$d_3>0,d_3<0$这两个简单的$\mathbb{Z}_2$分类.先找到一个绝热的插值$h(\theta)=d_0(\theta)\sigma^0+\sum_ad_a(\theta)\sigma^a$是定义在$d_3>,d_3<0$之间,自旋矢量$\vec{d}(\theta)$可以会沿着有粒子空穴对称决定的虚拟路径从北极点向南极点演化.

![png](/assets/images/topology/tpf6.png)

拓扑数$N_0[h_1,h_2]$可以简单的通过路径$d_a(\theta)$所包含的Berry位相来决定,当$h_1,h_2$在不同的极点是为$\pi$否则就是0.通过上面的例子就可以从图像上清晰的理解$\mathbb{Z}_2$的含义.

# 第二Chern数及其物理结果

根据前面的维度约化,从时间反演破缺$(2+1)$维的拓扑绝缘体通过第一Chern数进行分类,进而得到了$(1+1)\rightarrow(0+1)$维的对应理论.这里利用相同的维度约化方式从$(4+1)\rightarrow(3+1)\rightarrow(2+1)$维的链式来研究时间反演不变的拓扑绝缘体.

## $(4+1)$维中的第二Chern数及非线性响应

$(4+1)$维的绝缘体在外部$U(1)$规范场作用下会出现非线性响应,其系数对应着第二Chern数.它与前面$(2+1)$系统的Hall电导对应的第一Chern数是完全类似的.通过路径积分的方式来描述非线性响应是比较方便的,考虑一个耦合了$U(1)$规范场的$(4+1)$维哈密顿量

$$H[A]=\sum_{m,n}(c^\dagger_{m\alpha}h_{mn}^{\alpha\beta}e^{iA_{mn}}c_{n\beta}+\text{H.c})+\sum_mA_{0m}c^\dagger_{m\alpha}c_{m\alpha}$$

规范场$A^\mu$的有效作用量可以通过路径积分得到

$$e^{iS_\text{eff}[A]}=\int D[c]D[c^\dagger]\exp\{i\int dt[\sum_mc^\dagger_{m\alpha}(i\partial_t)c_{m\alpha}-H[A] \}=\text{det}[(i\partial_t-A_{0m})\delta^{\alpha\beta}_{mn}-h^{\alpha\beta}_{mn}e^{iA_{mn}}]$$

费米子系统的响应函数为

$$j_\mu({\bf x})=\frac{\delta S_\text{eff}[A]}{\delta A_\mu({\bf x})}$$

对于$(2+1)$维的情况,有效作用量$S_\text{eff}$包含了Chern-Simons项$(C_1/4\pi)A_\mu\epsilon^{\mu\nu\tau}\partial_\nu A_\tau$如公式(\ref{h2})所示,第一Chern数$C_1$出现在系数中.对于$(4+1)$维的系统,一个相似的拓扑项也会出现在有效作用量中,这就是第二Chern数

$$S_\text{eff}=\frac{C_2}{24\pi^2}\int d^4xdt\epsilon^{\mu\nu\rho\sigma\tau}A_\mu\partial_\nu A_\rho\partial_\sigma A_\tau$$

这里$\mu,\nu,\rho,\sigma,\tau=0,1,2,3,4$,这里的系数$C_2$可以通过计算单圈Feynamn图进行计算

![png](/assets/images/topology/tpf7.png)

$$C_2=-\frac{\pi^2}{15}\epsilon^{\mu\nu\rho\sigma\tau}\int\frac{d^4kd\omega}{(2\pi)^5}\text{Tr}[(G\frac{\partial G^{-1}}{\partial q^\mu})(G\frac{\partial G^{-1}}{\partial q^\nu})(G\frac{\partial G^{-1}}{\partial q^\rho})(G\frac{\partial G^{-1}}{\partial q^\sigma})(G\frac{\partial G^{-1}}{\partial q^\tau})]\label{ha10}$$

$q^\mu=(\omega,k_1,k_2,k_3,k_4)$是频率动量矢量,单粒子格林函数$G(q^\mu)=[\omega+i\delta-h(k_i)]^{-1}$.下面来研究第二Chern数$C_2$与非阿贝尔Berry位相规范场在动量空间中的联系.首先写出一些结论:

对于任何一个$(4+1)$维单粒子哈密顿量$h({\bf k})$的能带绝缘体,通过(\ref{ha10})定义的非线性响应系数$C_2$等于非阿贝尔Berry位相规范场在布里渊区(BZ)中的第二Chern数

$$C_2=\frac{1}{32\pi^2}\int d^4k\epsilon^{ijkl}\text{Tr}[f_{ij}f_{kl}],\quad f_{ij}^{\alpha\beta}=\partial_ia_j^{\alpha\beta}-\partial_ja_i^{\alpha\beta}+i[a_i,a_j]^{\alpha\beta},\quad a^{\alpha\beta}_i({\bf k})=-i\langle\alpha,{\bf k}\rvert\frac{\partial}{\partial k_i}\rvert\beta,{\bf k}\rangle\label{ha11}$$

这里$ij,k,l=1,2,3,4$.其中$a_i^{\alpha\beta}$中的$\alpha$是占据态的索引,因此对于一个一般的多带模型,$a_i^{\alpha\beta}$是个非阿贝尔规范场,$f_{ij}^{\alpha\beta}$与非阿贝尔场强相关联.**这里的关键点是将**(\ref{ha10})**简化成一个拓扑不变量,不论哈密顿量发生怎样的变化,只要能带不穿过费米能级,那么$C_2$就是不变的.**

先标记哈密顿量$h({\bf k})$的本征值$\epsilon_\alpha({\bf k}),\alpha=1,2,\cdots,N,\epsilon_\alpha({\bf k})\leq\epsilon_{\alpha+1}({\bf k})$.当有$M$条能带被占据的时候,从事可以对能带急性连续的形变$\epsilon_\alpha({\bf k})\rightarrow\epsilon_G$ for $\alpha\leq M,\epsilon_\alpha({\bf k})\rightarrow\epsilon_E$ for $\alpha>M,(\epsilon_E>\epsilon_G)$. 在变形的过程中,对应的所有本征态$\rvert\alpha,{\bf k}\rangle$都是不变的,也就是说可以把哈密顿量$h({\bf k})$变成一些平带模型.

![tpf8](/assets/images/topology/tpf8.png)

由于(\ref{ha10})与第二Chern数(\ref{ha11})都是拓扑不变量,下面对(\ref{ha11})研究其在平带上的性质,此时可以将哈密顿量写为

$$h_0({\bf k})=\epsilon_G\sum_{1\leq\alpha\leq M}\rvert\alpha,{\bf k}\rangle\langle\alpha,{\bf k}\rvert+\epsilon_E\sum_{\beta>M}\rvert\beta,{\bf k}\rangle\langle\beta,{\bf k}\rvert\equiv\epsilon_GP_G({\bf k})+\epsilon_EP_E({\bf k})$$

这里$P_G({\bf k})[P_E({\bf k})]$是占据态(空态)的投影算子.课题通过这些投影算子来定义非阿贝尔Berry联络,单粒子格林函数也可以通过投影算子来计算计算.综上可得,对于任意一个$(4+1)$维的能带绝缘体,这里总会有一个耦合$U(1)$规范场的有效作用量对应的Chern-Simons项,它的系数对应的正是非阿贝尔Berry位相规范场对应的第二Chern数.利用运动方程可以得到

$j^\mu=\frac{C_2}{8\pi^2}\epsilon^{\mu\nu\rho\sigma\tau}\partial_\nu A_\rho\partial_\sigma A_\tau\label{ha12}$

这是对外场$A_\mu$的非线性响应.当考虑下面的场时

$A_x=0,A_y=B_zx,A_z=-E_zt,A_w=A_t=0\label{ha16}$

这里$x,y,z,w$表示空间维度,$t$代表时间.非零分量的的场强度为$F_{xy}=B_z,F_{zt}=-E_z$,有(\ref{ha12})得到的电流为

$$j_w=\frac{C_2}{4\pi^2}B_zE_z$$

当沿着$x,y$方向进行积分之后(取周期边界条件且$E_z$不随$(x,y)$变化),可以得到

$$\int dxdyj_w=\frac{C_2}{4\pi^2}(\int dxdyB_z)E_z\equiv\frac{C_2N_{xy}}2\pi{E_z},$$

这里$N_{xy}=\int dxdy B_z/2\pi$是穿过$xy$平面的量子通量数目,这就是4D量子霍尔效应.第二Chern数为$C_2$的$(4+1)$维绝缘体,$zw$面上的量子Hall电导为$C_2N_{xy}/2\pi$,是由$xy$面上磁场磁通$2\pi N_{xy}$诱导出来的.第二Chern数同样可以通过研究表面态来理解,此时$(4+1)$维的表面态由$(3+1)$维的理论来描述.

## 基于Dirac模型的时间反演不变绝缘体

$(4+1)$维连续Dirac模型为

$$H=\int d^4 x[\psi^\dagger(x)\Gamma^i(-i\partial_i)\psi(x)+m\psi^\dagger\Gamma^0\psi],\quad i=1,2,3,4\text{是空间维度}$$

$\Gamma^\mu,\mu=0,1,2,3,4$是满足Clifford代数的Dirac矩阵

$$\{\Gamma^\mu,\Gamma^\nu\}=2\delta_{\mu\nu}\mathbb{I},\quad\mathbb{I}\text{是单位矩阵}$$

这个模型的格点形式为

$$H=\sum_{n,i}[\psi^\dagger_n(\frac{c\Gamma^--i\Gamma^i}{2})\psi_{n+\hat{i}}+\text{H.c}]+m\sum_n\psi^\dagger_n\Gamma^0\psi_n\label{ha15}$$

在动量空间中红

$$H=\sum_{\bf k}\psi^\dagger_{\bf k}[\sum_i\sin k_i\Gamma^i+(m+c\sum_i\cos k_i)\Gamma^0]\psi_{\bf k}\label{ha13}$$

将哈密顿量写成更紧凑的形式

$$H=\sum_{\bf k}\psi^\dagger_{\bf k}d_a({\bf k})\Gamma^a\psi_{\bf k},\quad d_a({\bf k})=[(m+c\sum_i\cos k_i),\sin k_x,\sin k_y,\sin k_z,\sin k_w]$$

与之前研究$(2+1)$维两带模型相似,单粒子哈密顿量形式为$h({\bf k})=d_a({\bf k})\Gamma^a$由两个本征值$E_{\pm}-\pm\sqrt{\sum_ad_a^2({\bf k})}$,不过此时能级是二重简并的,当$\sum_ad^2_a({\bf k})\equiv d^2({\bf k})$在整个BZ中不消失的时候,半满时系统是有能隙的,此时$E=E_{-}$的能带是占据的.因为此时有两个占据的能带,可以定义一个$SU(2)\times U(1)$的绝热联络.从哈密顿量(\ref{ha13})可以定义单粒子格林函数并计算第二Chern数

$$C_2=\frac{3}{8\pi^2}\int d^4k\epsilon^{abcde}\hat{d_a}\partial_x\hat{d_b}\partial_y\hat{d_c}\partial_z\hat{d_w}\partial_e\label{ha14}$$

**这是一个从BZ $T^4$到球$S^4$的映射**,$\hat{d_a}({\bf k})\equiv d_a({\bf k})/\rvert d({\bf k})\rvert$.由(\ref{ha14})所表示的winding number等于Berry位相规范场对应的第二Chern数.对于格点模型(\ref{ha15})可以简单计算其$C_2$.考虑格点模型有固定的正参数$c$和一个可调参数$m$,随着$m$的变化Chern数$C_2(m)$就是关于$m$的函数.当哈密顿量是无能隙的时候,Chern数就会发生变化$\sum_ad_a^2({\bf k})=0$.当$m\rightarrow+\infty$是矢量$\hat{d_a}({\bf k})=(1,0,0,0,0)$此时的$C_2(m)=0$.因此只需要研究$C_2(m)$发生变化的量子临界点即可,也就是$C_2(m)$发生变化时$m$的值.通过$\sum_ad_a^2({\bf k})=0$可以求解得到临界值$m$和对应的动量点${\bf k}$

$$m=\left\{\begin{array}{c}-4,\quad{\bf k}=(0,0,0,0)\\ -2c,\quad {\bf k}\in P[(\pi,0,0,0)]\\ 0,\quad\mathbf{k}\in P[(\pi,0,\pi,0)]\\ 2c,\quad \mathbf{k}\in P[(\pi,\pi,\pi,0)]\\ 4c,\quad\mathbf{k}=(\pi,\pi,\pi,\pi)\end{array}\right.$$

这里$P[\mathbf{k}]$表示通过交换波矢的索引得到的一系列矢量$\mathbf{k}$.比如$P[(\pi,0,0,0)]$包含了$(\pi,0,0,0),(0,\pi,0,0),(0,0,\pi,0),(0,0,0,\pi)$.下面研究一下临界点$m=-4c$处第二Chern数$C_2(m)$的变化.在$m+4c<<2c$的极限下,系统最小能隙位于$\mathbf{k}=0$,在该点进行低能展开可得$d_a({\bf k})\simeq (\delta m,k_x,k_y,k_z,k_w)+o(\rvert k\rvert),\delta m\equiv m+4c$.在动量空间中做截断$\Lambda<<2\pi$,可以得到第二Chern数在低能和高能部分

$$C_2=\frac{3}{8\pi^2}(\int_{\rvert\mathbf{k}\rvert<<\Lambda}+\int_{\rvert\mathbf{k}\rvert>>\Lambda})\epsilon^{abcde}\hat{d}_a\partial_x\hat{d}_b\partial_y\hat{d}_c\partial_z\hat{d}_d\partial_w\equiv C_2^{(1)}(\delta m,\Lambda)+C_2^{(2)}()\delta m,\Lambda$$

因为在高能部分$\rvert\mathbf{k}\rvert>\Lambda$不存在能级交叉,所以$C_2$在$\delta m=0$处的跃变仅仅来源于$C_2^{(1)}$,在极限$\rvert\delta m\rvert<\Lambda<<2\pi$时,通过连续近似的$d_a(\mathbf{k})$可得到

$$C_2^{(1)}(\delta m,\Lambda)\simeq\frac{3}{8\pi^2}\int_{\rvert\mathbf{k}\rvert<<\Lambda}d^4k\frac{\delta m}{(\delta m^2+\mathbf{k}^2)^{5/2}}$$

通过积分可以得到

$$\Delta C_{2\delta m=0^-}^{\delta m=0^+}=\Delta C_{2\delta m=0^-}^{(1)\delta m=0^+}=1$$

**从上面的分析可以知道第二Chern数由在能级交叉处有效连续模型来决定,在连续模型情况下对应的正是Dirac 模型.**对所有临界点附近进行分析可以得到

$$C_2(m)=\left\{\begin{array}{c}0,\quad m<-4c\quad\text{or}\quad m>4c\\ 1,\quad -4c<m<-2c\\ -3,\quad -2c<m<0\\ 3,\quad 0<m<2c\\ -1,\quad 2c<m<4c\end{array}\right.$$

在得到了第二Chern数之后,就可以通过拓扑非平庸的表面态来研究这个模型,与前面的研究方法相同,沿某一个方向取开边界,比如取$w$方向,其余的维度都是周期边界条件,哈密顿量可以转换成一个1D紧束缚模型的求和

$$H=\sum_{\vec{k},w}[\psi^\dagger_\vec{k}(w)(\frac{c\Gamma^0-i\Gamma^4}{2})\psi_\vec{k}(w+1)+\text{H.c}]+\sum_{\vec{k},w}\psi^\dagger_\vec{k}(w)[\sin k_i\Gamma^i+(m+c\sum_i\cos k_i)\Gamma^0]\psi_\vec{k}(w),$$

$C_2\neq 0$的能隙间表面态如下图所示

![tpf8](/assets/images/topology/tpf9.png)

当Chern数是$C_2$时,这里会有$C_2$支线性色散无能隙的表面态,其低能有效理论可以通过有$\rvert C_2\rvert$个手性费米子

$H=\text{sgn}(C_2)\int\frac{d^3 p}{(2\pi)^3}\sum_{i=1}^{\rvert C_2\rvert}v_i\psi^\dagger_i(\vec{p})\vec{\sigma}\cdot\vec{\mathbf{p}}\psi_i(\vec{p})$

前面的因子$\text{sgn}(C_2)$保证了表面态的手性,是由Chern数的符号决定的.从表面理论可以从更加物理的角度来理解外场$U(1)$规范场与非线性响应之间的关联.k考虑与(\ref{ha16})相同的规范场构型,则非零的场曲率为$F_{xy}=b_z,F_{zt}=-E_z$.最终一个$(3+1)$维表面态耦合磁场$\mathbf{B}=B_z\hat{\mathbf{z}}$和电场$\mathbf{E}=E_z\hat{\mathbf{z}}$,此时考虑$-4c<m<-2c$这个参数区间,对应的$cC_2=1$,此时的表面理论是手性费米子的单粒子哈密顿量

$$h=v\vec{\sigma}\cdot(\vec{p}+\vec{A})=v\sigma_xp_x+v\sigma_y(p_y+B_zx)+v\sigma_z(p_z-E_zt)$$

如果$E_z$足够小,此时时间依赖项$A_z(t)=-E_zt$可以看做是微扰,当$A_z$固定的时候单粒子能谱为

$$E_{n\pm}(p_z)=\pm v\sqrt{(p_z+A_z)^2+2n\rvert B_z\rvert},n=1,2,\cdots,\quad E_0(p_z)=v(p_z+A_z)\text{sgn}(B_z)$$

当表面取$L_x\times L_y\times L_z$的周期边界条件时,每个朗道能级的简并度为$N_{xy}=L_xL_yB_z/2\pi$.与量子Hall边界态的规范讨论相似,无限小的电场$E_z$将会绝热的移动动量$p_z\rightarrow p_z+E_zt$,如下图所示,从$t=0$到$t=T\equiv 2\pi/L_zE_z$时,动量的变化为$p\rightarrow p_z+2\pi/L_z$,此时3D表面上净增加的电子数目为$N_{xy}$,总而言之,一个一般的Hall流$I_w$个是沿着$w$方向的

$$I_w=\frac{N_xy}{T}=\frac{L_xL_yL_zB_zE_z}{4\pi^2}$$

![png](/assets/images/topology/tpf10.png)

根据电流密度可以得到$j_w=B_zE_z/4\pi^2$,这与前面得到的结果(\ref{ha12})一致.更加一般形式的电流密度$j_w$可以表示为

$$j_w=C_2\frac{\mathbf{E}\cdot\mathbf{B}}{4\pi^2}=\frac{C_2}{32\pi^2}\epsilon^{\mu\nu\sigma\tau}F_{\mu\nu}F_{\sigma\tau}$$

这是无质量$(3+1)$维Dirac费米子的手性反常方程.因为4D格点Dirac模型的3D无能隙边界态是手性费米子,所以电流$I_w$总是包含着特定手性的电荷,这将会导致3D边界上手性不守恒.
{:.info}

# 维度约化$(3+1)$维时间反演不变绝缘体

对于满足时间反演不变(TRI)的$(4+1)$维的体系其第二Chern数不为零,通过将其中的某个动量参数替换成$\theta$来实现维度约化的目的,从而可以来研究$(3+1)$维以及$(2+1)$维绝缘体.

## $(3+1)$维绝缘体的有效作用量

Dirac哈密顿量(\ref{ha15})耦合外部$U(1)$规范场之后

$$H[A]=\sum_{n,i}[\psi^\dagger_n(\frac{c\Gamma^0-i\Gamma^i}{2})e^{iA_{n,n+\hat{i}}}\psi_{n+\hat{i}}+\text{H.c}]+m\sum_n\psi^\dagger_n\Gamma^0\psi_n$$

现在考虑一个特殊的朗道规范$A_{n,n+\hat{i}}=A_{n+\hat{w},n+\hat{w}+\hat{i}}$,它沿着$w$方向是平移不变的,因此在周期边界条件下$w$方向的动量$k_w$是个好量子数,哈密顿量可以写为

$$H[A]=\sum_{k_w,\vec{x},s}[\psi^\dagger_{\vec{x},k_w}(\frac{c\Gamma^0-i\Gamma^s}{2})e^{iA_{\vec{x},\vec{x}+\hat{s}}}\psi_{\vec{x}+\hat{s},k_w}+\text{H.c}]+\sum_{k_w,\vec{x},s}\psi^\dagger_{\vec{x},k_w}\{\sin(k_w+A_{\vec{x}4})\Gamma^4+[m+c\cos(k_w+A_{\vec{x}4})]\Gamma^0\}\psi_{\vec{x},k_w}$$

这里的$\vec{x}$代表三维坐标,$A_{\vec{x}4}\equiv A_{\vec{x},\vec{x}+\hat{w}},s=1,2,3$表示$x,y,z$方向.在这个表达式中,不同$k_w$态是无耦合的,此时就可以将$(4+1)$的$H[A]$约化为一系列$(3+1)$维固定$k_w$的哈密顿量,重新改写$k_w+A_{\vec{x}4}=\theta_\vec{x}$约化到$(3+1)$维的模型为

$$H_{3D}[A,\theta]=\sum_{\vec{x},s}[\psi^\dagger_\vec{x}(\frac{c\Gamma^0-i\Gamma^s}{2})e^{iA_{\vec{x},\vec{x}+\hat{s}}}+\text{H.c}]+\sum_{\vec{x},s}\psi^\dagger_\vec{x}[\sin \theta_\vec{x}\Gamma^4+(m+c\cos \theta_\vec{x})\Gamma^0]\psi_\vec{x}\label{ha20}$$

着描述的是耦合电磁想$A_{\vec{x},\vec{x}+\hat{s}}$的能带绝缘体,绝热参数场为$\theta_\vec{x}$.为了研究$(3+1)$维系统的响应性质，有效作用量$S_\text{3D}[A,\theta]$为

$$\exp^{iS_\text{3D}[A,\theta]}=\int D[\psi]D[\bar{\psi}]\exp\{i\int dt[\sum_\vec{x}^{'}\bar{\psi}\vec{x}(i\partial_\tau-A_{\vec{x}0})\psi_\vec{x}-H[A,\theta]]\}\label{ha17}$$

在场构型$A_s(\vec{x},t)\equiv 0,\theta(\vec{x},t)\equiv\theta_0$处进行Taylor展开，$S_\text{3D}$中将会包含从$(4+1)$维推到得到的非线性响应

$$S_\text{3D}=\frac{G_3(\theta)}{4\pi}\int d^3xdt\epsilon^{\mu\nu\sigma\tau}\delta\theta\partial_\mu A_\nu\partial_\sigma A_\tau\label{ha18}$$

与(\ref{ha11})相比较，$\delta\theta(\vec{x},t)=\theta(\vec{x},t)-\theta_0$扮演了$A_4$的角色，系数$C_3(\theta)$可以通过相同的Feymann图来计算得到，只是此时需要对3D的哈密顿量(\ref{ha17})进行，不对$k_w$积分，最终可以得到$G_3(\theta)$的表达式

$$G_3(\theta)=-\frac{\pi}{6}\int \frac{d^3kd\omega}{(2\pi)^4}\text{Tr}\epsilon^{\mu\nu\sigma\tau}[(G\frac{\partial G^{-1}}{\partial q^\mu})(G\frac{\partial G^{-1}}{\partial q^\nu})(G\frac{\partial G^{-1}}{\partial q^\sigma})(G\frac{\partial G^{-1}}{\partial q^\tau})],\quad q^\mu=(\omega,k_x,k_y,k_z)$$

$G_3(\theta)$可以从Berry曲率中计算得到

$$G_3(\theta_0)=\frac{1}{8\pi^2}\int d^3k\epsilon^{ijk}\text{Tr}[f_{\theta i}f_{jk}]$$

此时Berry曲率是定义在四维空间中的$(k_x,k_y,k_z,k_\theta)$中，

$$a^{\alpha\beta}_i=-i\langle\vec{k},\theta_0;\alpha\rvert(\partial/\partial k_i)\rvert\vec{k},\theta_0;\beta\rangle,\quad a^{\alpha\beta}_\theta=-i\langle\vec{k},\theta_0;\alpha\rvert(\partial/\partial\theta_0)\rvert\vec{k},\theta_0;\beta\rangle$$

跟第二Chern数相比，可以得到求和规则

$$G_3(\theta)d\theta=C_2\in\mathbb{Z}$$

这正好对应着$(1+1)$维系统中泵浦系数求和$G_1(\theta)$，前面$G_1(\theta)=\partial P_1/\partial\theta$，这里$P_1$就是简单的电子极化。同样的在$(3+1)$维同样可以定义广义极化$P_3(\theta)$满足$G_3(\theta)=\partial P_3/\partial\theta_0$。通常情况下电子极化$\mathbf{P}$是与外部电场$\mathbf{E}$线性耦合的，磁化$\mathbf{M}$与外部磁场$\mathbf{B}$也是线性耦合的，然而此时可以看到$P_3$是一个赝标量，它与外部电磁场$\mathbf{E}\cdot\mathbf{B}$是非线性耦合的，因为这个原因通常称$P_3$是磁电极化。
{:.success}

为了得到$P_3$需要介绍非阿贝尔Chern-Simons项

$$\mathcal{K}^A=\frac{1}{16\pi^2}\epsilon^{ABCD}\text{Tr}[(f_{BC}-\frac{1}{3}[a_B,a_C])\cdot a_D]$$

这是一个四维空间$q=(k_x,k_y,k_z,\theta_0)$中的矢量，$A,B,C,D=x,y,z,\theta$，$\mathcal{K}$满足

$$\partial_A\mathcal{K}=\frac{1}{32\pi^2}\epsilon^{ABCD}\text{Tr}[f_{AB}f_{CD}]\rightarrow G_3(\theta_0)=\int d^3k\partial_A\mathcal{K}$$

当第二Chern数等于0时，在定义$a_A$的时候会遇到阻塞，也就意味在整个参数空间中$\mathcal{K}$不是单值的，然而在一个合适的规范选择下$\mathcal{K}$可以时单值的，$G_3(\theta)=\int d^3\partial_\theta\mathcal{K}^\theta\equiv\partial P_3(\theta_0)/\partial\theta_0$

$$P_3(\theta_0)=\int d^3k\mathcal{K}^\theta=\frac{1}{16\pi^2}\int d^3k\epsilon^{\theta ijk}\text{Tr}[(f_{ij}-\frac{1}{3}[a_i,a_j])\cdot a_k]$$

因此$P_3(\theta)$时非阿贝尔Chern-Simons项在三分量动量空间中的积分。这与电子极化时定义在一个动量空间中绝热演化路径的积分时相似的。

众所周知，Chern-Simons在三维的积分只有对整数取模才是规范不变的，在一个规范变换$a_i\rightarrow u^{-1}a_iu-iu^{-1}$下，极化$P_3$的改变为

$$\Delta P_3=\frac{i}{24\pi^2}\int d^k \epsilon^{theta ijk}\text{Tr}[(u^{-1}\partial_i u)(u^{-1}\partial_j u)(u^{-1}\partial_k u)]$$

它是一个整数，因此$P_3$就像$P_1$一样对1取模才是well defined，当改变$\theta_0$从0到$2\pi$就可以得到$C_2$。有效作用量(\ref{ha18})可以通过引入$G_3=\partial P_3/\partial\theta$进行简化，然后进行分部积分之后

$$S_{3D}=\frac{1}{4\pi}\int d^3kdt\epsilon^{\mu\nu\sigma\tau}A_\mu(\partial P_3/\partial\theta)v_\nu\delta\theta\partial_\sigma A_\tau\label{ha19}$$

这个有效的作用量对任意绝热依赖于$\vec{x},t$的哈密顿量$h(\vec{k},\vec{x},t)$都是well defined.这个有效作用量在场论中被称为轴子电动力学,绝热场$P_3$扮演了轴子场的作用.

## 有效作用量$S_{3D}$的物理效应

有效作用量是$A_\mu$的二次型,他描述了对外部电磁场的线性响应,而且这个场同时依赖于空间和$P_3$对时间的梯度.对$S_{3D}$求变分可以得到响应方程

$$j^\mu=\frac{1}{2\pi}\epsilon^{\mu\nu\sigma\tau}\partial_\nu P_3\partial_\sigma A_\tau\label{ha21}$$

下面可以从两种情况来理解上式的结果

### 空间梯度$P_3$诱导Hall效应

卡片绿亦歌系统$P_3=P_3(z)$仅在$z$方向变化,这个可以通过在Dirac模型(\ref{ha20})中变化$\theta=\theta(z)$,在这种情况下(\ref{ha21})变成

$$j^\mu=\frac{\partial_z P_3}{2\pi}\epsilon^{\mu\nu\rho}\partial_\nu A_\rho,\quad\mu,\nu,\rho=t,x,y$$

它描述了在$xy$平面上的量子霍尔效应,对应的Hall电导为$\sigma_{xy}=\partial_zP_z/2\pi$,如下图所示

![png](/assets/images/topology/tpf11.png)

对于一个在$x$方向均匀的电场$E_x$,Hall电流密度$j_y=(\partial_z P_3/2\pi)E_x$.沿着$z$方向有限区间急性积分就可以得到$xy$上的电流密度

$$J^{2D}_y=\int_{z_1}^{z_2}dzj_y=\frac{1}{2\pi}(\int_{z_1}^{z_2}dP_3)E_x$$

在区间$z_1\leq z\leq z_2$内的净Hall电导为

$$\sigma_{xy}^{2D}=\int_{z_1}^{z_2}dP_3/2\pi$$

在这个区间内它仅依赖于$P_3$的变化,与不依赖于其具体的细节$P_3(z)$.与$(1+1)$维的情况相似,如果对(\ref{ha8})进行空间积分,就可以得到由极化诱导出来的总电荷

$Q=-\int_{z_1}^{z_2}dP/2\pi$

通过比较可以发现在$(3+1)$维中的$P_3$与Hall电导间的关系与$(1+1)$维中极化与总电荷之间的关系式类似的.两个均匀材料将不同$P_3$处将会琮琤畴壁,从而由Hall电导为$\sigma_H=\Delta P_3/2\pi$.在$(1+1)$维中诱导的分数电荷为$Q=-\Delta P/2\pi$.

### $P_3$时间梯度诱导的拓扑磁电效应

当$P_3=P_3(t)$是空间均匀,但随着时间变化时,

$$j^i=-\frac{\partial_t P_3}{2\pi}\epsilon^{ijk}\partial_jA_k,\quad i,j,k=x,y,z,\quad\vec{j}=-\frac{\partial_tP_3}{2\pi}\vec{B}\label{ha22}$$

由于电荷极化$\vec{P}$满足$\vec{j}=\partial_t\vec{P}$,对于一个静态均匀的磁场B可以得到$\partial_t\vec{P}=-\partial_t(P_3\vec{B}/2\pi)$,因此有

$$\vec{P}=-\frac{\vec{B}}{2\pi}(P_3+\text{const})$$

这个方程描述了有磁场诱导的电子极化,正是磁电效应.与多铁材料中相同的效应相比较,此时的磁电效应是拓扑起源仅仅依赖于磁电极化$P_3$.与$(1+1)$维绝热泵浦效应相似,响应同样可以从表面态物理来理解,考虑一个格点Dirac模型(\ref{ha20})沿$x,y$方向是周期的$z$方向是开边界,当存在沿$z$方向的静态磁场$B_z$时,单粒子的能谱$E_n(\theta)$可以在固定$\theta$出进行求解,如上图(b)所示,在$(2+1)$维的边界上存在midgap states. 这里需要注意的是每个态都是$N$重简并的,$N=B_zL_xL_y/2\pi$是朗道能级简并度,在格点模型中当$-4c<m<-2c$时第二Chern数$C_2=\int^{\theta=2\pi}_{\theta=0}dP_3=1$可以发现在一个周期中$\theta=0\rightarrow2\pi$,$N$重简并的表面态在下边界下沉,然后再上边界浮出,当$\theta$绝热的从$0$到$2\pi$的过程中,将会有$N$个电子从上表面泵浦到下表面,这与前面(\ref{ha22})的结果是一致的

$$\Delta Q=\int dt\int dxdyj_z=-\frac{\int_0^{2\pi}dP_3}{2\pi}B_zL_xL_y=-NC_2$$

**在$(3+1)$维系统中磁场的绝热泵浦是$(4+1)$维拓扑绝缘体表面手性反常诱导的.**当磁单极存在的时候,拓扑词典效应将会存在特异的性质,对于一个均匀的$P_3$,方程(\ref{ha22})推导出

$$\nabla\cdot\vec{j}=-\frac{\partial_tP_3}{2\pi}\nabla\cdot\vec{B}$$

在格点上考虑紧致的$U(1)$电磁场,磁单极密度为$\rho_m=\nabla\cdot\vec{B}/2\pi$可以是非零的,可以得到

$$\partial_t\rho_e=(\partial_tP_3)\rho_m$$

因此当$P_3$绝热的从0变话到$\Theta/2\pi$,磁单极会获得一个电荷

$$Q_e=\frac{\Theta}{2\pi}Q_m$$

## $\mathbb{Z}_2$分类的时间反演不变绝缘体

在前面分析$(1+1)$维粒子空穴对称绝缘体中,关键是要找到两个满足粒子空穴对称的差值$h_1(k),h_2(k)$具有相同的Chern数宇称,这样他们相对Chern宇称就是well defined.此时3D系统具有的是时间反演对称,它会扮演与粒子空穴对称相同的作用.对于一个哈密顿量$H=\sum_{mn}c^\dagger_{m\alpha}h^{\alpha\beta}_{mn}c_{n\beta}$对应的时间反演变化时个反幺正算符$c_{m\alpha}\rightarrow T^{\alpha\beta}c_{m\beta}$,这里时间反演矩阵$T$满足$T^\dagger T=\mathbb{I},T^*T=-\mathbb{I}$,在动量空间中时间反演对称要求

$$T^\dagger h(-\vec{k})T=h^T(\vec{k})$$

$T^*T=-\mathbb{I}$是重要的,它将会导致Kramers简并,现在利用与前面$(1+1)$维相同的方法来对$(3+1)$维TRI的系统定义$\mathbb{Z}_2$不变量.对任意两个TRI的能带绝缘体$h_1(k),h_2(k)$,可以定义插值$h(k,\theta)$满足

$$h(k,0)=h_1(k),\quad h(k,\pi)=h_2(k),\quad T^\dagger h(-k,-\theta)T=h^T(k,\theta)$$

腿与$\theta\in [0,2\pi],h(k,\theta)$都是有能隙的.因为插值是$\theta$的周期函数,那么可以在$(k,\theta)$空间中定义Berry位相规范场的第二Chern数$C_2[h(k,\theta)]$.下面来研究对于任意两个插值$h,h^{'}$其$C_2[h(k,\theta)]-C_2[h^{'}(k,\theta)]=0\quad\text{mod}\quad 2$.定一辆个新的$g_{1,2}(k,\theta)$

$$g_1(k,\theta)=\left\{\begin{array}{c}h(k,\theta),\quad\theta\in [0,\pi]\\ h^{'}(k,2\pi-\theta),\quad\theta\in[\pi,2\pi]\end{array}\right.\\ g_2(k,\theta)=\left\{\begin{array}{c}h^{'}(k,2\pi-\theta),\quad\theta\in [0,\pi]\\ h(k,\theta),\quad\theta\in[\pi,2\pi]\end{array}\right.$$

通过定义,$g_1,g_2$满足$C_2[h]-C_2[h^{'}]=C_2[g_1]+C_2[g_2],T^\dagger g_1(-k,-\theta)T=g_2^T(k,\theta)$.为了研究$C_2[g_1]=C_2[g_2]$考虑$g_1(k,\theta)$的本征值为$E_\alpha(k,\theta)$的本征态$\rvert k,\theta;\alpha\rangle_1$

$$g_2^T(-k,-\theta)T^\dagger\rvert k,\theta;\alpha\rangle_1=T^\dagger g_1(k,\theta)\rvert k,\theta;\alpha\rangle_1=E_\alpha(k,\theta)T^\dagger\rvert k,\theta;\alpha\rangle_1\\ \rightarrow g_2(-k,-\theta)T^T(\rvert k,\theta;\alpha\rangle_1)^*=E_\alpha(k,\theta)T^T(\rvert k,\theta;\alpha\rangle_1)^*$$

因此$T^T(\rvert k,\theta;\alpha\rangle_1)^*$是$g_2(-k,\theta)$的本征态,其本征值也是$E_\alpha(k,\theta)$.将$g_2(-k,\theta)$的本征态$\rvert -k,-\theta,\beta\rangle_2$展开

$$T^T(\rvert k,\theta;\alpha\rangle_1)^*=\sum_\beta U_{\alpha\beta}(k,\theta)\rvert -k,-\theta;\beta\rangle_2$$

$g_1,g_2$系统的Berry位相规范矢量满足

$$a_{1j}^{\alpha\beta}(k,\theta)=-i\langle k,\theta;\alpha\rvert\partial_j\rvert k,\theta;\beta\rangle_1=-i[\sum_{\gamma,\delta}U^*_{\alpha\gamma}\langle -k,-\theta;\gamma\rvert\partial_j(U_{\beta\delta}\rvert -k,-\theta;\delta\rangle_2)]^*\\ =\sum_{\gamma,\delta}U_{\alpha\gamma}a_{2j}^{\gamma\delta*}(-k,-\theta)(U^\dagger)_{\delta\beta}-i\sum_\gamma U_{\alpha\gamma}(k,\theta)\partial_j U^*_{\beta\gamma}(k,\theta)\label{ha23}$$

总而言之$a_{1j}^{\alpha\beta}(k,\theta)$等于$a_{2j}^{\alpha\beta}$只是相差一个规范变换,Berry位相去曲率满足$f_{1ij}^{\alpha\beta}(k,\theta)=U_{\alpha\gamma}f^{\gamma\delta*}_{2ij}(-k,-\theta)(U^\dagger)_{\delta\beta}$,这就使得$C_2[g_1(k,\theta)]=C_2[g_2(k,\theta)]$.这里就证明了对任意两个对称插值$h,h^{'}$都有 $C_2[h(k,\theta)]-C_2[h^{'}(k,\theta)]=2C_2[g(k,\theta)]=0\quad\text{mod}\quad 2$,则相对第二Chern数宇称为

$$N_3[h_1(k),h_2(k)]=(-1)^{C_2[h(k,\theta)]}$$

它对任意两个时间反演不变的$(3+1)$维绝缘体都是well defined,与插值选取是无关的.与$(1+1)$ 情况相似,此时可以选取一个真空哈密顿量$h_0$作为参考,所有满足$N_3[h_0,h]=-1$的称为$\mathbb{Z}_2$非平庸,$N_3[h_0,h]=1$是平庸的.通过(\ref{ha23})的推导以及TRI哈密顿量满足$T^\dagger h(-k,-\theta)T=h^T(k,\theta)$,Berry位相规范势满足$a_i(k)=Ua_i(-k)U^\dagger-iU\partial_iU^\dagger$,从而可以得到电磁极化$P_3$满足

$$2P_3=\frac{i}{24\pi^2}\int d^3k\epsilon^{ijk}\text{Tr}[(U\partial_iU^\dagger)(U\partial_jU^\dagger)(U\partial_kU^\dagger)]\in\mathbb{Z}$$

这里仅有两个不等价TRI $P_3$值$P_3=0,P_3=1/2$.对两个哈密顿量$h_1,h_2$其第二Chern数满足$C_2[h(k,\theta)]=2(P_3[h_2]-P_3[h_1])$ mod 2,所以$P_3$的差值决定了相对Chern宇称$N_3[h_1,h_2]=(-1)^{2(P_3[h_1]-P_3[h_2])}$. 因此平庸的哈密顿量有$P_3=0$,而非平庸的为$P_3=1/2$.

当得到了$\mathbb{Z}_2$分类之后,由这个拓扑量子数对应的物理结果可以通过$S_{3D}=\frac{1}{4\pi}\int d^3xdt\epsilon^{\mu\nu\sigma\tau}P_3(x,t)\partial_\mu A)\nu\partial_\sigma A_\tau$来进行研究.一个粒子空穴对称$\mathbb{Z}_2$分类的绝缘体在其边界上将会存在零能束缚态,且边界上存在半整数电荷.同样的,对于非平庸的$(3+1)$维绝缘体同样由拓扑保护的表面态.而研究$(3+1)$维表面态最简单的方法就是再次进行维度约化.对于任意三维哈密顿量$h_1(k)$一个插值$h(k,\theta)$可以放置在$h_1$和真空哈密顿量$h_0$之间,如果把$\theta$看做是第四个动量,那么$h(k,\theta)$就定义了一个$(4+1)$维的能带绝缘体,而且它还要满足时间反演不变的限制.沿$z$方向取开边界条件,其余三个方向都是周期边界,当第二Chern数$\C_2[h]$非零时,在表面上此时将会有$\rvert C_2[h]\rvert$种$(3+1)$维手性费米子.也就是说在表面态的3D布里渊区中将会有$\rvert C_2[h]\rvert$个节点$(k_{xn},k_{yn},\theta_{n}),n=1,\cdots,\rvert C_2[h]\rvert$,这里的能谱$E_n(k_x,k_y,\theta)$是无能隙的并有线性色散的Dirac锥.

> 从时间反演对称可以得到$(k_x,k_y,\theta),(-k_x,-k_y,-\theta)$处的能谱是完全相同的,即如果$(k_x,k_y,\theta)$是节点则$(-k_x,-k_y,-\theta)$也一定是;**时间反演对称要求手性费米子一定是成对出现的,除了在时间反演不变动量点.**

![png](/assets/images/topology/tpf12.png)

当第二Chern数是奇数的时候,在3D布里渊区中一定有奇数个Dirac锥在八个高对称点上.

### $\mathbb{Z}_2$非平庸绝缘体物理性质

鱼油非平庸的绝缘体有磁电极化$P_3=1/2$ mod $1$, 根据

$$S_{3D}=\frac{1}{4\pi}\int d^3xdt\epsilon^{\mu\nu\sigma\tau}P_3(x,t)\partial_\mu A_\nu\partial_\sigma A_\tau\label{ha24}$$

体态有效作用量为

$$S_{3D}=\frac{2n+1}{8\pi}\int d^3xdt\epsilon^{\mu\nu\sigma\tau}\partial_\mu A_\nu\partial_\sigma A_\tau,\quad n=P_3-1/2\in\mathbb{Z}\label{ha25}$$

在时间反演对称下,$\epsilon^{\mu\nu\sigma\tau}\partial_\mu A_\nu\partial_\sigma A_\tau=2\mathbf{E}\cdot\mathbf{B}$是奇函数,有效作用量(\ref{ha24})破坏了时间反演对称.然而,当空间流形是闭合的时候(所有的方向都是周期边界),$\int d^3xdt\epsilon^{\mu\nu\sigma\tau}\partial_\mu A_\nu\partial_\sigma A_\tau$的结果是量子化的$8\pi^2m,m\in\mathbb{Z}$.y因此$S_{3D}=(2n+1)m\pi$,从而作用量$e^{iS_{3D}}=e^{im\pi}=(-1)^m$是时间反演不变的,而且与$n$无关(n是$P_3$的整数部分).因此在一个闭合的时空流形上,拓扑作用量(\ref{ha25})与$\mathbb{Z}_2$非平庸时间反演拓扑绝缘体的有效理论结果是一致的,极化$P_3$的整数部分并不是一个物理量.但是在开边界条件的时候,情况变的有所不同,在时空流形上有边界的时候$S_{3D}$的值不再是量子化的,基矢$P_3=1/2$ or $0$,在这种情况下$P_3$的整数部分并不会进入到$e^{iS_{3D}}$中并且物理,它的值会依赖于边界的具体细节.

为了理解开边界时候的物理,考虑在$z=0$两边分别是拓扑不等价的系统,有效作用量(\ref{ha24})可以写为

$$S_{3D}=\frac{1}{4\pi}\int d^3 xdt \epsilon^{\mu\nu\sigma\tau}A_\mu\partial_\nu P_3\partial_\sigma A_\tau$$

因为当$z<0P_3=1/2$ mod1 ,当$z>0$是$P_3=0$ mod 1,此时可以有

$$\partial_zP_3=(n+1/2)\delta(z)$$

这里的$n\in\mathbb{Z}$依赖于表面拓扑非平庸的细节.在这种情况下有效作用量可以约化到表面上$(2+1)$维的Chern-Simons项

$$S_\text{eff}=-\frac{2n+1}{8\pi}\int dxdydt\epsilon^{3\mu\nu\rho}A_\mu\partial_\nu A_\rho\label{ha26}$$

这与前面在$P_3$的畴壁上存在量子霍尔效应的结论一致.$\mathbb{Z}_2$非平庸绝缘体上表面上的Hall电导为$\sigma_H=(n+1/2)/2\pi$,它是一个半奇数乘以量子$e^2/h$.从上面分析中也可以得到在非平庸绝缘体表面上总是存在奇数个$(2+1)$维Dirac费米子.**因此表面上的半量子Hall效应可以从无质量Dirac费米子的宇称反常简单理解.**

> 由Dirac费米子携带的Hall电导只有在费米子质量不为零的时候才是well defined, 也就是说此时应该存在能隙.

联系哈密顿量模型$H=k_x\sigma^x+k_y\sigma^y+m\sigma^z$,其Berry曲率可以通过(\ref{c1})计算,矢量${\bf d}$为${\bf d}=(k_x,k_y,m)$其对应的Hall电导为

$$\sigma_H=\frac{1}{4\pi}\text{sgn}(m)(=\frac{e^2}{2h}\text{sgn}(m))$$

现在考虑拓扑绝缘体表面具有$(2n+1)$个无能隙的Dirac锥,从前面的讨论中可以知道,在不破坏时间反演对称的情况下,至少由一个Dirac锥是不打开能隙的,对每个Dirac锥考虑质量项$m_i,i=1,2,\cdots,2n+1$,诱导出的净Hall电导为$\sum_{i=1}^{2n+1}\text{sgn}(m_i)/4\pi$.由于$\sum_{i=1}^{2n+1}\text{sgn}(m_i)$s是奇整数,此时得到的Hall电导与Chern-Simons理论(\ref{ha26})得到的一致.从这个讨论同样可以理解有效作用量(\ref{ha26})描述了一个时间反演破缺的表面,尽管其体态仍然是时间反演不变的.

**体态的拓扑要求这里由1/2个量子的Hall电导,而表面的时间反演破缺则决定了整数部分n.**这个结论与粒子空穴对称$(1+1)$维系统终端会存在一个半整数的电荷是完全类似的.局域在绝缘体链一端的电荷为$(n+1/2)e$,整数部分$n$依赖于时间反演破缺的表面,而$1/2$则是由体态拓扑
所保证的.
{:.success}

下面从更加明确的物理角度来研究这个表面态,通过一个Dirac格点模型来作为例子,考虑一个$(3+1)$维的格点模型(\ref{ha20}),并且有一个$\theta(\vec{x})$畴壁存在

$$\theta(\vec{x})=\theta(z)=\frac{\pi}{2}[1-\tanh(z/4\xi)],\quad \theta(z\rightarrow-\infty)=\pi,\theta(z\rightarrow+\infty)=0$$

其构型如下图所示

![png](/assets/images/topology/tpf13.png)

当沿着$x,y$方向为周期边界时,哈密顿量可以进行块对角化

$$\begin{equation}\begin{aligned}H&=\sum_{z,k_x,k_y}[\psi^\dagger_{k_x,k_y}(z)(\frac{c\Gamma^0-i\Gamma^3}{2})\psi_{k_x,k_y}(z+1+\text{H.c})]\\&+\sum_{z,k_x,k_y}\psi^\dagger_{k_x,k_y}(z)[(m+c\cos\theta(z)+c\cos k_x+c\cos k_y)\Gamma^0+\sin k_x\Gamma^1+\sin k_y\Gamma^2]\psi^\dagger_{k_x,k_y}(z)\\&+\sum_{z,k_x,k_y}\psi^\dagger_{k_x,k_y}(z)\sin\theta(z)\Gamma^4\psi^\dagger_{k_x,k_y}(z)\equiv H_0+H_1\end{aligned}\end{equation}\label{ha27}$$

在时间反演变化下$\Gamma^0$是偶函数$\Gamma^{1,2,3,4}$是奇函数性质,因此(\ref{ha27})中只有最后一项是时间反演奇函数项,因为$\sin\theta(z)$项的存在,它会局域点边界上.将哈密顿量分解为$H=H_0+H_1$,这里$H_1$代表的就是(\ref{ha27})中的最后一项,而$H_0$则是其余满足TRI的项.第一$h_0,h_1$分别对应$H_0,H_1.哈密顿量$H_0$描述$\theta=0,\theta=\pi$交接处的时间反演不变面.对于$-4c < m < -2c$参化的哈密顿量$H_0(\theta),\theta\in[0,2\pi]$有一个Chern数$C_2=1$,因此对于$\theta=0,\theta=\pi$的系统有相对Chern宇称为-1.可以进行检验对于$\theta=0,-4c < m < -2c$哈密顿量与$m\rightarrow-\infty$是绝热连接的.因此$\theta=0,\theta=\pi$对应的分别是$\mathbb{Z}$的拓扑平庸与非平庸相.因此对于$H_0$在$z$的畴壁处,会存在奇数个无能隙的Dirac锥.通过数值的方式同样可以确定对于$h_0$在$(k_x,j_y)=(0,0)$存在一个Dirac锥.接下来研究$h_1$的作用,它满足$\{\Gamma^4,h_0=0\}$满足反对易关系,则是一个质量项,表面Dirac锥的有效哈密顿量为$h)\text{surf}=k_x\sigma_x+k_y\sigma_y$是个合适的基矢,它与$\GAmma^4$反对易.在希尔伯特空间中与$H_\text{surf}$反对易的项只有$\sigma_z$,因此在格点模型中$\Gamma^4$的作用是诱导出质量项$m\sigma_z$.更加准确的关于$m$的幅值和符号可以通过微扰理论进行计算.$H-\text{surf}$的两个零能表面态为$\rvert k=0,\alpha\rangle,\alpha=1,2$,在有效理论中矩阵$\sigma_x,\sigma_y$的表示为

$$\sigma_{\alpha\beta}^{i}=\langle k=0,\alpha\rvert\frac{\partial h_0}{\partial k_i}\rvert_{k=0}\rvert k=0,\beta\rangle,\quad i=x,y$$

$\sigma_z$可以表示为$-i\sigma_x\sigma_y$,因此质量m由

$$m=\frac{1}{2}\sum_{\alpha\beta}\sigma_{\alpha\beta}^z\langle k=0,\beta\rvert h_1\rvert k=0,\alpha\rangle$$

决定.考虑一个参数化的哈密顿量$h=h_0+\lambda h_1$,表面Drirac费米子的质量在$\lambda\rightarrow 0$的时候正比于$\lambda$. 如上图(c)所示, 当$\lambda<0$的时候表面Hall电导为$\text{sgn}(\lambda)/4\pi.$表面Hall电导同样可以从有效理论进行计算. 对于$\lambda=1$位相场$\theta$从$\pi$变到$0$,对应的Hall电导为$\sigma_H=\int_{-\infty}^{+\infty}dP_3(z)/2=\int_0^\pi dP_3(\theta)/2\pi=-1/4\pi$.对于$\lambda=-1$可以考虑将$H(\theta)$中的$\theta(z)$替换成$-\theta(z)$,这个操作保持了$h_0$不变但是改变了$h_1$的符号,最终是的$\theta$的winding从$-\pi$变到了$0$,对应的Hall电导为$\sigma_H=\int_{-\pi}^0dP_3(\theta)/2=1/4\pi$.这两种情况对应的$\theta$的winding如上图(d)所示.

物理上,时间反演对称破缺项来源于磁场或者表面上的局域磁矩(可能来源于表面相互作用导致的自发时间反演对称破缺).一旦这样的"时间反演破缺表面场"(M)出现,有效作用量$S_{3D}=\frac{1}{4\pi}\int d^3 xdt \epsilon^{\mu\nu\sigma\tau}A_\mu\partial_\nu P_3\partial_\sigma A_\tau$在开边界的时候是well defined, 它描述了$\mathbb{Z}_2$非平庸绝缘体对电磁场的响应. 实际上,时间反演破缺场应该被认为是施加在TRI系统上的外场,此时有效作用量$S_{3D}$描述的是一个结合M和电磁场$A_\mu$系统的非线性响应.对于一个占据空间大小为$\mathcal{V}$的$\mathbb{Z}_2$非平庸系统,其边界为$\partial\mathcal{V}$,$P_3$的空间梯度为

$$\nabla P_3(\vec{x})=(g[M(\vec{x})]+\frac{1}{2})\int_{\partial\mathcal{V}}d\hat{\bf n}\delta^3(\vec{x}-\vec{y})$$

这里$g[M(\vec{x})]\in\mathbb{Z}$是有时间反演破缺场$M(\vec{x})$决定的winding的整数部分,$\hat{\bf n}$是表面的法线方向.在这种$\nabla P_3$的构型下$S_{3D}$可以约化成表面Chern-Simons作用量

$$S_\text{surf}=\frac{1}{4\pi}\int_{\partial\mathcal{V}}d\hat{n}(g[M(\vec{x})]+\frac{1}{2})\epsilon^{\mu\nu\sigma\tau}A_\nu\partial_\sigma A_\tau\label{ha28}}$$

因为通常$g[M(\vec{x})]$只能取离散的值,非平庸绝缘体表面将会有几个畴壁对应着不同的Hall电导.

#### 磁化诱导量子Hall效应
![png](/assets/images/topology/tpf14.png)

考虑如上图所示的两层题词层具有平行或者反平行的磁化方向,一个标准的六终端设置可以执行平面Hall电导的测量,净Hall电导是有上下两个表面的和贡献的.当拓扑绝缘体是均匀的时候,一个外指向的磁化矢量将会有相同的效应,无论那个表面上存在这样的磁化.假设上面有电场$\mathbf{E}=E_x\hat{\bf x}$诱导的Hall电流$\mathbf{j}_t=\hat{\bf n}_t\times \mathbf{E}/4\pi$,下表面与上表面的公式相同$\mathbf{j}_b=\hat{\bf n}_b\times  \mathbf{E}/4\pi$.因为上下表面的法线方向相反$\hat{\bf n}_t=-\hat{\bf n}_b=\hat{\bf z}$,电流满足$\mathbf{j}_t=-\mathbf{j}_b$,如上图所示.最终,反平行磁化诱导出净为零的Hall电流,平行磁化诱导出的$\sigma_H=e^2/h$.和整数量子Hall效应相同,这里量子化的Hall电导是由手性边界态贡献的.由图14(a)可以看到,磁化矢量在上下表面上的方向是相反的,虽在在全局$x,y,z$基矢上磁化方向是相同的,但是通过每个面上的法线方向$\hat{\bf n}$来定义,两个表面上的Hall电导是相反的.也就是说在表面Chern-Simons有效作用量(\ref{ha28})中,对上表面而言$g[M(\vec{x})]$是$0$但是对下表面则是$-1$.结果就是在两个表面的边界交界处就会有Hall电导.这就类似于通常量子霍尔系统中在$\nu=0$和$\nu=1$的区域内,在畴壁处会补货手性费米流体,这正是实验上锁观测到的净Hall效应.

> 这里边界面是两维的,所以一般情况下除了一致手性的边界态之外,同样会有其他无寿星的传播模式,但是这些无手性的态并不会改变净的稳定的手性边界态,因此这里总是会存在一支向左或者向右运动的边界态.

这些边界态的稳定性是受到体态能隙保护的,在此时是有磁化诱导的能隙$E_M$.在满足下面两个要求的情况下是可以观测到这种效应的:

- 温度$k_BT << E_m$
- 当化学势在由磁化诱导上下表面能隙之间

#### 拓扑磁电效应
拓扑磁电效应是由$P_3$诱导出来,可以通过(\ref{ha22})与$\vec{P}=-\frac{\vec{B}}{2\pi}(P_3+\text{const})$描述,接下来考虑在非平庸拓扑绝缘体中实现这种效应.和表面量子Hall效应相同,$P_3$的整数部分是由磁化决定的,考虑一个铁磁-拓扑绝缘体-铁磁的异质结,入托14(b)所示,因为具有反平行的磁化,电场$E_x$诱导的电流在上下表面上的方向是相反的.当考虑一个如上描述的没有Hall bar的孤立系统,形成了一个循环的电流,在电场的作用下会诱导出平行或者反平行的磁化.然而当考虑图14(b)所示的几何结构时,循环电流在无能隙的边界面上会有耗散,违反了拓扑磁电(TME)的绝热条件.为了得到TME需要在边界面上存在破坏时间反演的能隙,这个可以通过图15(a)中的圆柱形结构来实现.

![png](/assets/images/topology/tpf15.png)

在圆柱体的表面上存在指向面外的磁化还有固定的Hall电导$\sigma_H=(n+\frac{1}{2})e^2/h$.当平行于圆柱体施加一个电场后,在边界面上就会诱导出沿着切线方向的循环电流,其强度为$j_t=\sigma_HE$.这个循环电流的出现与在表面上束缚一个常数的磁化$M=j_t/c=(n+1/2)\frac{e^2}{hc}E$是相同的,它的方向与电场是反平行的.总之,表面的Hall电流就像是拓扑磁化电流,表面的半Hall效应就等价于体态磁化贡献的拓扑

$$\mathbf{M}_t=-(n+\frac{1}{2})\frac{e^2}{hc}\mathbf{E}$$

这里需要指出的是,响应系数等于$1/4\pi$成精细结构常数$\alpha=e^2/\hbar c$的奇数倍.通常情况下如果一个电场施加在方向方向为$\hat{\bf n}$的拓扑绝缘体表面上行,Hall电流为$\mathbf{j}_H=(n+1/2)\frac{e^2}{h}\hat{\bf n}\times\mathbf{E}$, 这与上式给出的磁化产生的磁化流是一致的.结合通常非拓扑的磁化响应$\mathbf{M}_c$,可以得到总的磁化为$\mathbf{M}=\mathbf{M}_c+\mathbf{M}_t$,则修改后的方程为

$$\mathbf{H}=\mathbf{B}-4\pi\mathbf{M}_c+(2n+1)\frac{e^2}{\hbar c}\mathbf{E}\label{ha29}$$

同样的电场和磁场的诱导也会发生在平行于圆柱体施加磁场的情况下,如图15(b)所示.当磁场从零逐渐打开时,平行于边界面的循环电流将会被产生,诱导出的Hall电流为$j\simeq dB/dt$,其方向会平行或者反平行与磁场方向.最终,在上下表面会有正比于磁场$B$的电荷密度积累,因此又磁场诱导电荷极化的拓扑贡献为

$$\mathbf{P}_t=(n+\frac{1}{2})\frac{e^2}{hc}\mathbf{B}$$

将常规与拓扑的响应结合起来可以得到

$$\mathbf{D}=\mathbf{E}+4\pi\mathbf{P}_c-(2n+1)\frac{e^2}{\hbar c}\mathbf{B}\label{ha30}$$

通常的Maxwell's方程加上(\ref{ha29})和(\ref{\ha30})就可以完整的描述3D拓扑绝缘体的电动力学.另外一个替代描述就是利用常规的关系$\mathbf{D}=\mathbf{E}+4\pi\mathbf{P}_c$和$\mathbf{H}=\mathbf{B}-4\pi\mathbf{M}_c$外加上一些被拓扑相修正的Maxwell's方程.包含拓扑相$S_{3D}=\frac{1}{4\pi}\int d^3xdt\epsilon^{\mu\nu\sigma\tau}P_c(x,t)\partial_\mu A_\nu\partial_\sigma A_\tau$后的电磁场总的作用量为

$$S_\text{tot}=S_\text{Maxwell}+S_\text{topo}=\int d^3xdt[\frac{1}{16\pi}F_{\mu\nu}F^{\mu\nu}+\frac{1}{2}F_{\mu\nu}\mathcal{P}^{\mu\nu}-\frac{1}{c}j^\mu A_\mu]+\frac{\alpha}{16\pi}\int d^3xdt P_3\epsilon^{\mu\nu\sigma\tau}F_{\mu\nu}F_{\sigma\tau}\label{ha32}$$

$\alpha\equiv e^2/\hbar c$是精细结构常数,$\mathcal{P}^{0i}=P^i,\mathcal{P}^{ij}=\epsilon^{ij}M_k$分别是电,磁极化矢量.可以通过对$A_\mu$求变分得到运动方程

$$\frac{1}{4\pi}\partial_\nu F^{\mu\nu}+\partial_\nu\mathcal{P}^{\mu\nu}+\frac{\alpha}{4\pi}\epsilon^{\mu\nu\sigma\tau}\partial_\nu(P_3F_{\sigma\tau})=\frac{1}{c}j^\mu$$

这些方程可以写成更加熟悉的形式

$$\nabla\cdot\mathbf{D}=4\pi\rho+2\alpha(\nabla P_3\cdot\mathbf{B})\\ \nabla\times\mathbf{H}-\frac{1}{c}\frac{\partial\mathbf{D}}{\partial t}=\frac{4\pi}{c}\mathbf{j}-2\alpha((\nabla P_3\times \mathbf{E})+\frac{1}{c}(\partial_t P_3)\mathbf{B})\\ \nabla\times\mathbf{E}+\frac{1}{c}\frac{\partial\mathbf{B}}{\partial t}=0\\ \nabla\cdot\mathbf{B}=0\label{ha31}$$

这里$\mathbf{D}=\mathbf{E}+4\pi\mathbf{P}_c,\mathbf{H}=\mathbf{B}-4\pi\mathbf{M}_c$仅仅包含了非拓扑的贡献. 这些是轴子电动力学的运动方程.通过将拓扑项移动到左边,并根据(\ref{ha20})和(\ref{ha30}重新改写$\mathbf{D,H}$,取$P_3=n+1/2$就可以得到传统的Maxwell's方程.

**因为在拓扑绝缘体中体态存在时间反演对称,不可能由其他非拓扑的机制来对磁电系数由贡献,这也保证了拓扑磁电效应的鲁棒性.**

这里要强调一下,在拓扑绝缘体中$P_3$的值只有在当打开能隙的表面上存在磁化的时候才能被确定,如图15(c),选择一个路径$L$从参考点深入到真空中,$P_3$可以被计算$P_3(\vec{x})=\int_{\vec{x}_0L}^{\vec{x}}dl\cdot \nabla P_3$.然而这个结果仅仅适用于当结果不依赖于路径的时候.如果一个磁化的壳包裹在拓扑绝缘体表面上,在界面的任何处磁化方向都指向外侧,当$P_3$穿过界面的时候在不同位置处的改变量都是相同的,此时体态的$P_3$是well defined,在这种情况下,方程(\ref{ha29},\ref{ha30})也都是well defined,如果磁化的方向反向,那么$P_3$的整数部分会发生改变.另一方面,当在表面上存在磁化方向的畴壁时,在体态中此时整数部分的$P_3$不是well defined,(\ref{ha29},\ref{ha30})并不能使用,如图15(d)所示.方程(\ref{ha29},\ref{ha30}})失败是因为此时边界上存在量子霍尔边界流,此时需要更加一般形式的Maxwell's方程(\ref{ha31})来包含这些边界电流的贡献.这些分析同样提供了表面Hall效应新的图像,即表面上的量子霍尔效应是由寄居在$P_3$场vortex ring上的手性边界态产生的.只有当这种边界态不存在,表面是full gapped,电磁响应才可以用(\ref{ha29},\ref{ha30})来描述.

#### 低频Faraday旋转
通过一个电容施加电场,并利用超导量子干涉仪来探测磁场从而可以观测TME效应,同样的也可以利用Faraday或者Kerr旋转来进行探测.修改后的Maxwell方程(\ref{ha31})可以运用到地外一个现象中-光子传播系统.这里需要注意方程(\ref{ha32})只能应用到力能极限$E << E_g$,这里$E_g$是表面态的能隙.用来探测系统拓扑性质的光子频率应该是低频光子$\omega << E_g/hbar$.

![png](/assets/images/topology/tpf16.png)

在$z=0$处考虑一个铁磁-拓扑绝缘体的界面,如上图所示,正常的线性偏振光可以表示为

$$\mathbf{A}(z,t)=\left\{\begin{array}{c}\mathbf{a}e^{i(-kz-\omega t)}+\mathbf{b}e^{i(kz-\omega t)},\quad z>0\\ \mathbf{c}e^{i(-k^{'}z-\omega t)},\quad z<0\end{array}\right.$$

这里的$k=\omega/v,k^{'}=\omega/v^{'}$分别是$z>0,z<0$区域的波矢. 方程(\ref{ha32})中的$\nabla P_3$项在$z=0$处会贡献一个非常规的边界条件.定义$\nabla P_3=\Delta\hat{\bf z}\delta(z)$(满足$\Delta -1/2\in\mathbb{z}$),边界条件为

$${\bf a+b=c},\quad \hat{\bf z}\times [k(-\mathbf{a}+\mathbf{b})/\mu+k^{'}\mathbf{c}/\mu^{'}]=-\frac{2\alpha\Delta\omega}{c}\mathbf{c}$$

这里$\epsilon,epsilon^{'}$和$\mu,\mu^{'}$分别是$z>0,z<0$处的的介电常数和透射率.简记$a_\pm=a_x\pm ia_y,b_\pm,c_\pm$也一样,上面的方程可以得到

$$a_+=\frac{1}{2}[1+\frac{k^{'}/\mu^{'}-2i\alpha\Delta\omega/c}{k/\mu}]c_+$$

当入社波矢$\mathbf{a}$是线极化的,那么传播波矢$\mathbf{c}$同样是线极化的,极化平面的旋转角度为

$$\theta_\text{topo}=\arctan\frac{2\alpha\Delta}{\sqrt{\epsilon/\mu}+\sqrt{\epsilon^{'}/\mu^{'}}}\label{ha33}$$

这里总是假设铁磁材料的磁化方向是垂直于$xy$面的,因此$\mathbf{H}=\mu\mathbf{B}$总是一个面内的磁场.

由于铁磁材料同时也会诱导Fraday旋转,在测量拓扑贡献(\ref{ha33})的时序必须对其进行区分,将铁磁层替换成具有更大磁化率的顺磁材料并施加磁场进行极化,此时磁化正比于磁场,因此体态贡献的Faraday旋转正比于磁场.净Faraday旋转为$\theta=\theta_\text{topo}^{(t)}+\theta_\text{topo}^{(b)}+\theta_\text{bulk}$,它与磁场的依赖关系为

$$\theta(B)=\mu B+2\text{sgn}(B)\arctan\frac{2}{\sqrt{\epsilon/\mu}+\sqrt{\epsilon^{'}/\mu^{'}}}$$

最终,拓扑贡献可以通过改变磁场的方向来得到,也可以通过外推$\theta(B)$在$B\rightarrow 0^+$的极限下.

# 维度约化zhi$(2+1)$维














# 参考

- 1.[Topological field theory of time-reversal invariant insulators](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.78.195424)
