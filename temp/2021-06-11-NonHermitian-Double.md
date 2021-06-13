---
title: 两维非厄米体系中的Fermion Doubling Theorems
tags: Topology Non-Hermitian
layout: article
license: true
toc: true
key: a202106010
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
这篇博客想通过精读一片研究两维非厄米体系中的Fermion Doubling Theorems的PRL文章,同时了解厄米与非厄米体系中的Fermion Doubling Theorems到底是什么.
{:.info}
<!--more-->
在学习凝聚态中的拓扑的时候,总是看到Weyl点是要成对出现的(不过也有了一些材料研究,可以让Weyl点单独出现),这是背后由比较深刻的物理,涉及格点规范场论,暂时功力不够看不懂,我还没有完全理解,因为相关的文章比较老;不过最近在活跃的非厄米体系中开始研究Fermion Doubling Theorems问题,我感觉和Weyl点成对出现是有关联的,所以准备借这篇非厄米的文章来学习一下这个概念,**如有大佬清楚这里面的联系,还请不吝赐教**.
# Fermion doubling
`当简单得尝试将一个费米子场放置到格点上的时候,就会出现一些虚假的状态,这样一来,每个原始的费米子会出现2d个费米子粒子,这里d是系统的维度.`

下面利用凝聚态的语言理解一下,假定是利用连续模型来描述能带,那么在$\Gamma=(0,0)$的时候,模型是个massless的Dirac方程,在这个点就有Dirac费米子,当把连续模型变成紧束缚模型之后,就会把原本的无限大的空间$k\rightarrow+\infty$限制到第一布里渊区中,假定是正方点整,那么在布里渊区中的每个角落处于中心$\Gamma$点是等价的,此时在这些点上再对紧束缚模型做低能展开,同样可以得到连续模型,只不过此时前面的系数会出现一个负号,或者不出现负号,也就是说在格点模型上Fermion的数目不再是一个了,这也就是Fermion doubling.
## Mathematica overview
在$d$维的时候考虑质量为$m$的自由Dirac费米子,其作用量为

$$S=\int d^dx\bar{\psi}(i\gamma_\mu a^\mu-m)\psi$$

这里的$\gamma_\mu$就是gamma矩阵,当把这个作用量离散化到立方格点上之后,费米子场$\psi(x)$就变成了离散的形式$\psi_x$,此时的$x$表示的是格点位置.而原本的导数则变成有限差分,作用量变为

$$S=a^d\sum_{x,\mu}\frac{i}{2a}(\bar{\psi}_x\gamma_\mu\psi_{x+\hat{\mu}}-\bar{\psi}_{x+\hat{\mu}}\gamma_\mu\psi_x)-a^d\sum_{x}m\bar{\psi}_x\psi_x$$

这里的$a$是格点间距,$\hat{\mu}$是沿着$\mu$方向的单位矢量,当在动量空间中计算时

$$S^{-1}(p)=m+\frac{i}{a}\sum_\mu\gamma_\mu\sin(p_\mu a)$$

因为实空间中的格点间距$a$是有限的,则动量$p_\mu$限制在布里渊区中,通常取第一布里渊区$[-\pi/a,\pi/a]$.

在$S^{-1}$中令$a\rightarrow 0$的时候,就可以得到正确的连续模型下的结果,但是当在布里渊区角落($\pi/2$)处展开这个表达式的时候,可以发现同样会得到连续模型的结果,只不过此时会在gamma矩阵前面发生符号改变.这也就一维着,当动量的某一个分量在$\pi/a$附近的时候,离散的费米子场的行为同样会与连续情形下的费米子相同,这可以发生在动量空间动量的所有$d$个分量上,相比于原来连续模型的Dirac费米子,这里会有$2^d$中不同"味道"的费米子.

在格点哈密顿量的能谱中,这些拓扑点一定是成对出现的,这样会避免在格点上有量子反常的出现,因为对于单个的节点,它的低能物理是由量子反常的场论来描述的,如果成对出现,则反常会相互抵消,比如在石墨烯中双重节点对应的Dirac点与磁性Weyl半金属中成对出现的Weyl点.**在任何格点哈密顿量的体态中,doubling theorem一定会是满足的,但是在格点表面上可能会违反,**比如拓扑绝缘体有时间反演对称存在后,其表面只有一个宇称反常的Dirac点.这个反常的表面态则会导致恨到新奇的物理现象出现.

# Non-Hermitian
对于非厄米体系,其哈密顿量不再满足厄米共轭$H^\dagger\neq H$,此时会存在三种不同的节点:
- (1)费米点Fermi points(FPs)
- (2)奇异点exceptional points(EPs)
- (3)合格简并点nondefective degeneracy points(NDPs).

在EP和NDP两个能带在简并点是简并的,但是在EP点的时候,会存在波函数坍塌(虽然简并度是两重的,但是简并态只有一个),然而在NDP处本两个简并态的波函数是不同的.因此对于非厄米系统而言,哈密顿量在EPs是不可对角化的,只能约化成Jordan block的形式,如下图所示

![png](..assets\images\Non-Hermitian\fd1.png)

**当不存在对称性的时候,FPs和EPs在2维是拓扑稳定的,这也就意味着这些节点是不可以通过微扰被移除的**.

考虑一个非厄米的哈密顿量$\mathcal{H}(\mathbf{k})$,其复数能带是well-separate,除了在某些可能的简并点,这些简并点要么是EPs要么是NDPs.为了在非厄米体系中证明doubling theorems,需要依赖于:拓扑点会附带非零的拓扑荷,由于周期性的存在,在整个布里渊区中它们的求和一定是零

$$\sum_{k_i\in BZ}C(\mathbf{k}_i)=0$$

这里的$C(\mathbf{k}_i)$代表的是在BZ中的$\mathbf{k}_i$处的拓扑荷,它是沿着顺时针方向的一个包含EP或者FP的闭合路径对拓扑荷密度的积分得到的.

对于FPs一个何时的电荷密度是$\text{det}[\mu-\mathcal{H}(\mathbf{k})]$取对数球导数,而对于EPs则是$\mathcal{H}(\mathbf{k})$相对于能量E的判别式取对数然后求导.

研究同样发现对于3维体系,在其表面上是可以违反doubling theorem的,这同样说明3维的体态能带具有不寻常的性质.特别是当存在反演对称或者反射对称的系统,可以在表面上存在单个的FPs或者
EPs,所以在其体态一定存在Fermi lines或者exception lines.

# Doubling theorem for FPs
对于非厄米哈密顿量$\mathcal{H}(\mathbf{k})$其对应的复能带为$E_i(\mathbf{k})$.哈密顿量的FPs对应着在布里渊区中复化学势与某一个能带相交对应的$\mathbf{k}^j_F\rightarrow \mu-E_i(\mathbf{k}^j_F)=0$.通过选择何时的基矢,可以使的在整个布里渊区中能谱都是单只的,则PFs的位置可以通过$\mathcal{H}(\mathbf{k})$的特征多项式来得到

$$f_\mu(\mathbf{k})\equiv\text{det}[\mu-\mathcal{H}(\mathbf{k})]=\Pi_i[\mu-E_i(\mathbf{k})]\label{a3}$$

多项式$f_\mu(\mathbf{k})=0$的解就是FPs的位置,因为此时是个复多项式,则会给出两个条件$\text{Re}[f_\mu(\mathbf{k})=0],\text{Im}[f_\mu(\mathbf{k})]=0$,它们的解会对应两条闭合的线,其交点对应的就是FPs的位置,如下图(a1)所示

![png](..\assets\images\Non-Hermitian\fd2.png)

这里可以发现两个闭合的线总是相交偶数次,这也就是FPs的doubling theorem.当在哈密顿量中引入微扰之后,仅仅是会影响必和路径的形状,但是不会使得FPs消失.

下面通过更加数学的方式来描述拓扑不变量,定义一个全局的winding number不变量

$$W(\mathbf{k}_F^j)=\frac{i}{2\pi}\oint_{\Gamma(\mathbf{k}_F^j)}d\mathbf{k}\cdot\nabla_\mathbf{k}\ln f_\mu(\mathbf{k})\label{a1}$$

这里的积分路径是包含$\mathbf{k}_F^j$沿顺时针方向的闭合路径,如上图(b1)所示.因为多项式$f_\mu(\mathbf{k})$在整个布里渊区中都是单值的,每个winding number$W(\mathbf{k}_F^j)$也都是量子化的整数,在每个FP点处$\mathbf{k}_F^j$都会对应的由一个拓扑荷.**当winding number不等于零的时候,积分路径$\Gamma(\mathbf{k}_F^j)$不能平滑的收缩成一个点,因为它包含了一个奇异点.**这也就保证了在FP点处的拓扑稳定性,从而微扰不能打开能隙.当对整个布里渊区中所有的FPs对应的winding number求和之后

$$\sum_{\mathbf{k}_F^j\in BZ}W(\mathbf{k}_F^j)=\frac{i}{2\pi}\oint_{\partial BZ}d\mathbf{k}\cdot\nabla_\mathbf{k}\in f_\mu(\mathbf{k})=0\label{a2}$$

上面的求和一定等于零,因为在方程(\ref{a1})中的积分路径可以连续的变形为布里渊区的边界$\partial BZ$,在金粉中只有FPs是具有奇异性的.因此每个带有正拓扑荷的FP点一定伴随着一个带有负拓扑荷的FP点出现.
## 具体实例
这里通过一个两能带模型来对FPs点进行研究.

$$\mathcal{H}(\mathbf{k})=h_0(\mathbf{k})\sigma_0+{\bf h(k)\cdot\sigma},\quad h_0(\mathbf{k})=\frac{1}{2}\sin k_y,h_x(\mathbf{k})=\sin k_x-i,\\ h_y(\mathbf{k})=\sin k_y,h_z(\mathbf{k})=\cos k_x+\cos k_y -2$$

当化学势为$\mu=\sqrt{3}/4$的时候两个FPs位置为$\mathbf{k}_F^{-}=(0,-0.479\pi),\mathbf{k}_F^{+}=(0,\pi/2)$,对应的winding number为$W(\mathbf{k}_F^{\pm})=\mp 1$,此时是满足doubling theorem的.哈密顿量$\mathcal{H}(\mathbf{k})$的能谱为$E_\pm(\mathbf{k})=(s_y/2)\pm\sqrt{5-4(c_x+c_y)+c_{x+y}+c_{x-y}-2is_x}$.这里记号$c_{x/y}=\cos k_{x/y},s_{x/y}=\sin k_{x/y},c_{x\pm y}=\cos (k_x\pm k_y)$.这个能谱是多值的,且存在brach cut终止与两个EPs处,在$(0,\pm\pi/3)$处的能量为$E-\mu=0,E-\mu=-\sqrt{3}/2$.

又是后会遇到EPs和FPs出现在相同的位置,这纯属偶然,通常情况下载一般的非厄米哈密顿量中,两者是处在不同位置的.

# 判别式与DPs
下面来研究非厄米哈密顿量中的简并点(DP),并通过特征多项式$f_E(\mathbf{k})$的判别式来快速寻找简并点.这里$f_E(\mathbf{k})$的定义为(\ref{a3}),但是化学势会被$E$代替.一个DP点$\mathbf{k}_D$出现在$E_i(\mathbf{k}_D)=E_j(\mathbf{k}_D),i\neq j$,因此多项式$f_E(\mathbf{k})$在$\mathbf{k}_D$一定会有多个根,多项式的判别式定义为

$$\text{Disc}_E[\mathcal{H}](\mathbf{k})=\Pi_{i<j}[E_i(\mathbf{k})-E_j(\mathbf{k})]^2$$

一定会在$\mathbf{k}_D$处消失,当DP出现在$\mathbf{k}_D$处,一定会有$\text{Disc}_E[\mathcal{H}](\mathbf{k}_D)=0$.从判别式来计算DPs相比于求解多项式$f_E(\mathbf{k})$的根要更有效率.判别式可以通过计算$f_E(\mathbf{k})$和$\partial_Ef_E(\mathbf{k})$的Sylvester矩阵的行列式得到,因此利用判别式$\text{Disc}_E[\mathcal{H}](\mathbf{k})$的零值来寻找整个布里渊区中所有的DPs是最有效的方法.

判别式还有一个额外的优点,它是单值的,因为多项式$f_E(\mathbf{k})$的系数都是单只的,这个性质在根据$\text{Disc}_E[\mathcal{H}](\mathbf{k})$定义量子化不变量的时候很重要,对证明doubling theorem也同样重要.首先来给出说明性的一个解释为什么DPs一定会满足doubling theorme.可以发现判别式的零点一定会满足两个限制$\text{Re}[\text{Disc}_E[\mathcal{H}](\mathbf{k})]=0,\text{Im}[\text{Disc}_E[\mathcal{H}](\mathbf{k})]=0$.通过这两个等式可以在布里渊区中确定两个闭合的线,他们的交点就是DPs的位置,而布里渊区是具有周期性的,那么这两条线的交点数目也一定会是偶数次,因此DPs一定也是成对出现的,从而满足doubling theorem.

在不存在额外对称性的时候,DPs一般只存在两重简并,热河一个具有高简并度的DPs可以通过加入一个微扰,是的分开成多对具有双重简并的DPs.
{:.warning}

# Doubling theorem for DPs
一个DPs可以使EPs或者NDPs,它的拓扑表征不变量,可以根据沿着判别式进行积分的结果来确定

$$\nu(\mathbf{k}_D^l)=\frac{i}{2\pi}\oint_{\Gamma(\mathbf{k}_D^l)}d\mathbf{k}\cdot\nabla_\mathbf{k}\ln\text{Disc}_E[\mathcal{H}](\mathbf{k})\label{a4}$$

这里$\Gamma(\mathbf{k}_D^l)$是包含在$\mathbf{k}_D^l$处DP的一个顺时针路径,因为$\text{Disc}_E[\mathcal{H}](\mathbf{k})$是单值的,这个不变量是量子化的,叫做判别式数.它的数学结构与FPs的winding number是相同的,唯一的区别就是在积分中将$\text{det}[\mu-\mathcal{H}(\mathbf{k})]$替换成了$\text{Disc}_E[\mathcal{H}](\mathbf{k})$.非零的$\nu$值保证了DPs对于能隙的打开具有稳定性，利用方程







# 参考
- 1.[Fermion Doubling Theorems in Two-Dimensional Non-Hermitian Systems for Fermi Points and Exceptional Points](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.126.086401)
- 2.[Fermion doubling](https://en.wikipedia.org/wiki/Fermion_doubling)
- 3.[Jordan matrix](https://en.wikipedia.org/wiki/Jordan_matrix)


