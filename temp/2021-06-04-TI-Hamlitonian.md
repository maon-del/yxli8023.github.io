---
title: 拓扑绝缘体哈密顿量推导
tags: Topology Group Theory
layout: article
license: true
toc: true
key: a20210609
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
这篇博客整理一下在拓扑材料Bi$_2$Se$_3$计算中,通过能带成分和对称性分析,再结合微扰论来推导低能有效模型.
{:.info}
<!--more-->
虽然对拓扑绝缘体的材料和对应的模型都很熟了,但是始终没有掌握如何从具体的材料出发,来得到其对应的低能哈密顿量,从而可以在材料的基础上,对模型进行研究.这里就想通过精读[Model Hamiltonian for topological insulators](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.82.045122)这篇文章,来掌握一下这个方法.
# 晶体结构
首先来明确材料Bi$_2$Se$_3$的晶体结构等信息.首先在[Material Project](https://materialsproject.org/)这个网站中找到这个材料,其晶体结构时菱形的,对应的空间群是$D_{3d}^5(R\bar{3}m)$,其晶体结构如下图所示,沿着$z$方向是个层状结构,每个元胞中有5个原子,

![png](..\assets\images\topology\tih1.png)

两个蓝色标记的等价Bi原子(Bi1,Bi$1^{'}$),两个绿色标记的等价Se原子(Se1,Se$1^{'}$),还有一个黄色的Se原子,它与Se1原子是不等价的,5个原子层构成一个元胞,通常被称为quintuple layer.

沿着$z$方向看,每个原子层都形成了三角晶格,而且每一层的排列方式都是不同的.

![png](..\assets\images\topology\tih2.png)

沿着$z$方向,这些三角层以$A-B-C-A-B-C-\cdots$的方式进行堆叠,此时元胞基矢$t_i,i=1,2,3$并不是沿着$z$方向的.比如在五元层中Se2原子占据了$A$位置,那么在下一个五元层他就会占据$c$或者$B$,而不会继续占据$A$位置.这里直角坐标轴的选取如下:$z$方向是垂直于原子层的,$x$轴是沿着一个二元轴,具有两重旋转对称,$y$轴是沿着等分线轴,它是反射面与Se2原子层的交线.
# 对称性
这个晶体结构具有下面的一些离散对称性:
- 沿$z$方向三重旋转$R_3^z$
$R_3^z$可以通过下面的变换产生:$x\rightarrow x\cos\theta-y\sin\theta,y\rightarrow x\sin\theta+y\cos\theta,z\rightarrow z,\theta=\frac{2\pi}{3}$
- 沿着$x$方向的两重旋转$R_2^x$
这个操作对应着$x$方向不动,$z,y$方向都反演,$x\rightarrow x,z\rightarrow -z,y\rightarrow -y$,此时原子层的变换为$Se2\rightarrow Se2,Bi1\rightarrow Bi1^{'},Se1\rightarrow Se1^{'}$,在这个操作下发现原子层Bi1(Se1)和Bi1'(Se1')相互交换了位置.
- 反演对称$P$
以Se2位置作为反演中心,$Se2\rightarrow Se2,Bi1\rightarrow Bi1^{'},Se1\rightarrow Se^{'}$,在反演操作下Bi1(Se1)变换到$Bi1^{'}(Se1^{'})$.
- 时间反演对称$\mathcal{T}$
时间反演操作为$\mathcal{T}=\Theta\mathcal{K},\Theta=i\sigma_2,\mathcal{K}$是复数共轭,这里$\sigma_i$矩阵代表的是自旋.
# 原子轨道
为了从物理图像上理解$Bi_2Se_3$的能带结构,首先来研究每个元素的轨道信息.Bi原子的电子结构维$6s^26p^3$,Se的为$4s^24p^4$,**可以发现两种元素最外层电子都是$p$轨道的,因此在考虑能带的时候,就可以只关心$p$轨道电子的贡献,而忽略其余轨道**.因为$Bi_2Se_3$是个层状结构,在单个的五元层中,化学键是比较强的,但是在相邻两个五元层之间仅通过较弱的范德瓦尔斯力耦合在一起,因此可以只关心单个五元层的信息.在一个五元层中又一个元胞中存在5个原子,前面也提到过只需要关注$p$轨道即可($p_x,p_y,p_z$),因此这里一个元胞中会有15个轨道,首先忽略电子自旋,在之后考虑自旋轨道耦合(SOC)时再进行自旋的研究.这里标记一下轨道$\rvert\Lambda,\alpha\rangle,\Lambda=Bi1,Bi1^{'},Se1,Se1^{'},Se2,\alpha=p_x,p_y,p_z$.通过晶体结构可以发现,$Se2$在五元层的中间,被夹在两层Bi($Bi1,Bi1^{'}$)之间,而两个$Se(Se1,Se1^{'})$位于最外层.**由于所有的Se原子层都被Bi原子层分开了,所以体系中耦合最强的就是Bi原子层与Se原子层**.这样的耦合会产生能级排斥效应,使得$Bi$的能级被推高形成新的态$\rvert B_\alpha\rangle,\rvert B^{'}\rangle$,而$Se$的能级则被压低形成三个态$\rvert S_\alpha\rangle,\rvert S_\alpha^{'}\rangle,\rvert S0_\alpha\rangle$,如下图所示.

![png](..\assets\images\topology\tih3.png)

因为系统具有反演对称,可以方便的讲这些轨道组合,形成具有确定宇称的成键态与反键态

$$\rvert P1^\pm,\alpha\rangle=\frac{1}{\sqrt{2}}(\rvert B_\alpha\rangle\mp\rvert B^{'}_\alpha\rangle),\quad \rvert P2^\pm,\alpha\rangle=\frac{1}{\sqrt{2}}(\rvert S_\alpha\rangle\mp\rvert S^{'}_\alpha\rangle)$$

这里上标的正负号对应着态的宇称,$\alpha=p_x,p_y,p_z$.当$\rvert B_\alpha(S_\alpha)\rangle$与$\rvert B^{'}_\alpha(S^{'}_\alpha)\rangle$之间的耦合被考虑之后,成键态与反键态对应的能量劈裂来,反键态比成键态具有更高的能量,如上图II阶段所示.此时$\rvert P1^+,\alpha\rangle,\rvert P2^-,\alpha\rangle,(\alpha=p_x,p_y,p_z)$是靠近费米面的,所以可以只关注这些态,而忽略那些远离费米面附近的能带的贡献.因为晶体是个层状结构,在原子平面上$z$方向与$x,y$方向是不同的,因此对$P1^+,P2^-$态,$p_z$轨道的能量分离与$p_x,p_y$轨道是不同的.这里$\rvert P1^+,p_{x,y}\rangle$轨道的能量比$\rvert P1^+,p_z\rangle$的能量高,而$\rvert P2^-,p_{x,y}\rangle$比$\rvert P2^-,p_z\rangle$的能量低,因此导带只考虑$\rvert P1^+,p_z\rangle$,价带只考虑$\rvert P2^-,p_z\rangle$,如上图III所示.


在上面的原子轨道的基础上开始考虑SOC效应,给每个态再赋予自旋指标,态$\rvert P1^+,\alpha,\sigma\rangle,\rvert P2^-,\alpha,\sigma\rangle$都是双重简并的,$\sigma=\uparrow,\downarrow$表示的是自旋.原子的SOC哈密顿量为$\hat{H}_{SOC}=\lambda{\bf s\cdot L},\lambda=\frac{1}{2m_0^2c^2r}\frac{\partial U}{\partial r}$依赖于原子的势场$U$,它会将原子的轨道和自旋耦合起来.将轨道$p_x,p_y$转换成$p_\pm$来定义轨道角动量

$$\rvert \Lambda,p_+,\sigma\rangle=-\frac{1}{\sqrt{2}}(\rvert\Lambda,p_x,\sigma\rangle+i\rvert\Lambda,p_y,\sigma\rangle),\quad\rvert \Lambda,p_{-},\sigma\rangle=\frac{1}{\sqrt{2}}(\rvert\Lambda,p_x,\sigma\rangle-i\rvert\Lambda,p_y,\sigma\rangle),\quad\Lambda=P1^+,P2^-$$

在这个基矢下,原子SOC的哈密顿量为

$$\langle\Lambda,p_+,\uparrow\rvert H_{SOC}\rvert\Lambda,p_+,\uparrow\rangle=\langle\Lambda,p_{-},\downarrow\rvert H_{SOC}\rvert\Lambda,p_{-},\downarrow\rangle\equiv\frac{\lambda_\Lambda}{2}\\ \langle\Lambda,p_+,\downarrow\rvert H_{SOC}\rvert\Lambda,p_+,\downarrow\rangle=\langle\Lambda,p_{-},\uparrow\rvert H_{SOC}\rvert\Lambda,p_{-},\uparrow\rangle\equiv-\frac{\lambda_\Lambda}{2}\\ \langle\Lambda,p_+,\downarrow\rvert H_{SOC}\rvert\Lambda,p_z,\uparrow\rangle=\langle\Lambda,p_{-},\uparrow\rvert H_{SOC}\rvert\Lambda,p_{z},\downarrow\rangle\equiv\frac{\lambda_\Lambda}{2}\\ \langle\Lambda,p_z\uparrow(\downarrow)\rvert\rvert H_{SOC}\rvert\Lambda,p_z,\uparrow(\downarrow)\rangle=0 $$



# 参考

- 1.[Model Hamiltonian for topological insulators](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.82.045122)
