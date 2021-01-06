---
title: WannierTools计算Chern绝缘体性质
tags:  vasp
layout: article
license: true
toc: true
key: a20210106a
pageview: true
sitemap: true
mathjax: true
author: YuXuan
show_author_profile: true
---
之前我用WannierTools计算过了Weyl半金属的一些性质,不过那是从一个连续模型出发然后自己构造的紧束缚格点模型,这里我想通过自己最近重新研究的Chern insulator模型来更加具体的学习一下WannierTools的使用,同时也想对Chern Insulator这个模型通过计算一些拓扑的性质来加深自己对这个模型的理解和认识.
{:.info}
<!--more-->
# Chern Insulator
Chern Insulator这个模型还是很简单的,没有任何对称性去保护它,其对应的哈密顿量为
$$
\begin{equation}
H(\mathbf{k})=A_x\sin(k_x)\sigma_x+A_y\sin(k_y)\sigma_y+(m_0-t_x\cos(k_x)-t_y\cos(k_y))\sigma_z
\end{equation}
$$
当$m_0\in(-2,2)$的时候这个体系都是具有边界态的,也就是说它是拓扑的,那么我们就可以分别计算其对应的Berry曲率,Wannier Charge Center(WCC),以及通过表面格林函数计算其边界态,下面我就详细的记录一下如何将一个紧束缚模型的哈密顿量变成WannierTools需要的数据格式.
# 模型变数据
要明白这个变换过程,请自行学习紧束缚近似模型和Wannier波函数这两个相关的内容,可以参考固体理论(李正中)这本书.
要将紧束缚近似模型改写到实空间中的`Wannier`轨道上,也就是做下面的变换
$$
\begin{equation}
\sin(k)=\frac{1}{2i}(e^{ik}-e^{-ik})\\
\cos(k)=\frac{1}{2}(e^{ik}+e^{-ik})\\
c_i=\frac{1}{\sqrt{\mathcal{N}}}\sum_{k}e^{-ik}c_k
\end{equation}
$$
也就是将$k$空间的哈密顿量要在实空间的`Wannier`波函数上来计算不同近邻格点之间波函数的overlap,能看懂紧束缚近似模型,肯定就清楚如何从`sin,cos`变成离散的格点形式,所以这里直接了当的认为$e^{ik_x}$就是就是电子在$x$正方向上的hopping,那么相应的$e^{-ik_x}$则是代表电子在$x$负方向上的hopping.

下面再来对泡里矩阵$\sigma$进行分析理解,因为这里讨论的是一个2轨道模型,也就是一个2带模型,所以$\sigma_x$相关的项就表示轨道间(带间)耦合是简并的,而对于$\sigma_y$则轨道间(带间)的耦合是相反的,最后对于$\sigma_z$这一项,是不存在轨道间(带间)耦合的.

所以对于$t_x\cos(k_x)\sigma_z$,来将它代表的实空间中`Wannier`波函数的overlap详细的表示出来,它代表着轨道1自己于自己在$x$正方向上的hopping大小是$t_x/2.0$,而在$x$负方向上hopping的大小也是$t_x/2.0$.其余各项的分析和这个都是相同的,至于$m_0$则是代表了on-site的能量,也就是没有hopping.这里的$1/2.0$是来自于将$\cos$利用欧拉公式变化时引入的.所以对于这一项,可以将它写作
```fortran
ir = ir + 1  !ir在这里只是一个简单的计数变量
hmnr(1, 1, ir) = -tx/2.0
hmnr(2, 2, ir) = tx/2.0
```
对应的将$A_x\sin(k_x)\sigma_x$也可以写成上面的形式,这里的$\sigma_x$就代表着是轨道间的耦合,且这个耦合是简并的
```fortran
hmnr(1, 2, ir) = ax/(2.0*im)
hmnr(2, 1, ir) = ax/(2.0*im)
```
其余的所有项也是按照上面的变换方式写出来的,整理一个Fortran的程序来将上面的过程集合到一起,程序如下
```fortran
! Chern insulator
! usage:
! compile and run
! gfortran writeHmnR.f90 -o writehmnr
! ./writehmnr
! H  = Ax sin(kx)s_x+Ay sin(ky)s_y + (m0 - tx cos(kx) - ty cos(ky))s_z
program writeHmnR
implicit none
integer, parameter :: dp=kind(1d0) ! 双精度计算
complex(dp), parameter :: im = (0d0, 1d0) ! 虚数单位i
complex(dp), parameter :: zzero = (0d0, 0d0)
integer :: i, j
integer :: ir
integer :: nwann
!> arrays for hamiltonian storage
integer :: nrpts
integer, allocatable :: ndegen(:)
integer, allocatable :: irvec(:, :)
complex(dp), allocatable :: hmnr(:, :, :)

!> three lattice constants
real(dp) :: Ax,Ay,m0,tx,ty
Ax = 1d0
Ay = 1d0
m0 = 1d0
tx = 1d0
ty = 1d0

nwann = 1 ! 构建紧束缚模型时候Wannier轨道的数目,由Chern绝缘体的哈密顿量可以看出这里由两个轨道,只有一个轨道是占据的 
nrpts = 17
allocate(irvec(3, nrpts)) ! Chern insulator是个2D模型,所以hopping的方向也就只有2个,所以在之后的设置中保持第三个方向上恒为0
allocate(ndegen(nrpts))
allocate(hmnr(nwann*2, nwann*2, nrpts))
irvec = 0
ndegen = 1 ! 手动设置紧束缚模型数据所需要
hmnr = zzero


! 0 0 onsite能量
ir = 1  ! ir用来记录这里一共会有多少个hopping的方位(包括了onsite)
irvec(1, ir) =  0
irvec(2, ir) =  0
hmnr(1, 1, ir) = m0 
hmnr(2, 2, ir) = -m0

!1 0 x正反向hopping
ir = ir + 1
irvec(1, ir) =  1
irvec(2, ir) =  0

hmnr(1, 1, ir) = -tx/2.0
hmnr(1, 2, ir) = ax/(2.0*im)
hmnr(2, 1, ir) = ax/(2.0*im)
hmnr(2, 2, ir) = tx/2.0

!-1 0 x负方向hopping
ir = ir+ 1
irvec(1, ir) = -1
irvec(2, ir) =  0

hmnr(1, 1, ir) = -tx/2.0
hmnr(1, 2, ir) = -ax/(2.0*im)
hmnr(2, 1, ir) = -ax/(2.0*im)
hmnr(2, 2, ir) = tx/2.0

! 0 1 y正方向hopping
ir = ir + 1
irvec(1, ir) =  0 
irvec(2, ir) =  1

hmnr(1, 1, ir) = -ty/2.0
hmnr(1, 2, ir) = -im*ay/(2.0*im)
hmnr(2, 1, ir) = im*ay/(2.0*im)
hmnr(2, 2, ir) = ty/2.0

!0 -1  y负方向hopping
ir = ir + 1
irvec(1, ir) =  0 
irvec(2, ir) = -1

hmnr(1, 1, ir) = -ty/2.0
hmnr(1, 2, ir) = im*ay/(2.0*im)
hmnr(2, 1, ir) = -im*ay/(2.0*im)
hmnr(2, 2, ir) = ty/2.0

nrpts = ir

!> write to new_hr.dat
open(unit=105, file='ChernInsulator_hr.dat')
write(105, *)'Chern Insulator'
write(105, *)nwann*2
write(105, *)nrpts
write(105, '(15I5)')(ndegen(i), i=1, nrpts)
do ir = 1, nrpts
   do i = 1, nwann*2
      do j = 1, nwann*2
         write(105, '(5I5, 2f16.8)')irvec(:, ir), i, j, HmnR(i, j, ir)
      end do
   end do
end do
close(105)
stop
end ! end of program 
```
到这里就将一个紧束缚的哈密顿量完全转换成了WannierTools所需要的紧束缚的紧束缚的数据.