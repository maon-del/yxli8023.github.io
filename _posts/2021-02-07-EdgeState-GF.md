---
title: 利用格林函数求解边界态
tags: Code Method Julia Topology
layout: article
license: true
toc: true
key: a20210207b
header:
  theme: dark
  background: 'linear-gradient(135deg, rgb(34, 139, 87), rgb(139, 34, 139))'
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
pageview: true
aside:
    toc: true
sitemap: true
mathjax: true
author: YuXuan
show_author_profile: true
---
这里是利用边界格林函数方法来计算边界态,相比于通常取cylinder的方法,计算速度上是要快一些,做出来的图可以更加清晰的反映边界态的特征.
<!--more-->
在之前的[Hamiltonian构建时的基矢选择](https://yxli8023.github.io/2020/07/03/Basis-Chose.html)这篇博客中,虽然是和哈密顿量基矢选择有关的问题,但是我同样展示了如何通过一个紧束缚哈密顿量来计算拓扑边界态,虽然这个方法也很常见,用的也比较多,但是有时候为了反映一些局部的特征,可能需要把开边界的格点数目取的非常大,这就会使的计算量变得很大,耗时较长,这里就想利用边界格林函数的方法来计算边界态,它的优点是此时需要的矩阵维度是很小的,主要就是进行迭代计算,如果所需要的精度合适,计算速度上的提升是非常客观的,而且可以将边界态的某些细节反映的非常好,这里就整理一下如何利用边界格林函数来计算这样的边界态.

# 模型方法
这里选用BHZ模型

$$H(\mathbf{k})=(m_0-t_x\cos k_x-t_y\cos k_y)\sigma_z+\lambda_x\sin k_x\sigma_xs_z+\lambda_y\sin k_y\sigma_y\label{ham}$$

计算方法如下,已经知道了$H$之后,系统的格林函数可以写作

$$G^{-1}(z)=z-H=\left(\begin{array}{cccc}
z-H_0&C&0&0\\
C^\dagger&z-H_0&C&0\\
0&C^\dagger&z-H_0&C\\
0&0&C^\dagger&\cdots
\end{array}\right)\label{gf}$$

where the diagonal block H0 describes the Hamiltonian within the same “principal layer,”这一项其实就是哈密顿量(\ref{ham})沿某一方向开边界之后,包含好量子数$k_i$的那部分,自然$C,C^\dagger$就是相邻格点之间的hopping项了,从这里就可以看出,这样哈密顿量需要处理的就只是很小的一块,计算量自然很小.

我们可以发现由于(\ref{gf})是个三对角形式,所以可以将它通过迭代的方式进行求解

$$g^{(N)}_{ij}=(z-H_0-Cg^{(N-1)}C^\dagger)^{-1}_{ij}$$

对于初始条件

$$g^{(0)}=(z-H_0)^{-1}$$

他就是系统的边界格林函数,当选择一定的迭代精度之后,就可以求解得到最后的边界格林函数$g^{(N)}$,通过格林函数就可以计算对应的谱函数,也就可以得到边界态的结果

$$A(\omega,k_i)=-\frac{1}{\pi}\textrm{Im}(g^{(N)}(\omega,k_i))$$

结果如下图

![png](/assets/images/Julia/edge-gf.png)

这里计算得到的图像并不是很光滑,这与计算的时候选择的计算间隔以及格林函数中的小虚部有关,而且和作图工具也有关系,不过我最近在学习利用gunplot来做图,因为是命令作图,基矢数据量非常大也不同担心电脑死机,而用类似origin的前端作图工具,当想让曲线光滑的时候,所需要的数据文件就会非常大,从而对电脑要求就会非常高,所以可以通过这些方面的改进来将这个图做得更好看.
{:.warning}

# 代码
## Julia
```julia
using LinearAlgebra,DelimitedFiles,PyPlot
#---------------------------------------------------
function Pauli()
    hn = 4
    g1 = zeros(ComplexF64,hn,hn)
    g2 = zeros(ComplexF64,hn,hn)
    g3 = zeros(ComplexF64,hn,hn)
    #------ Kinetic energy
    g1[1,1] = 1
    g1[2,2] = -1
    g1[3,3] = 1
    g1[4,4] = -1
    #-------- SOC-x
    g2[1,2] = 1
    g2[2,1] = 1
    g2[3,4] = -1
    g2[4,3] = -1
    #---------- SOC-y
    g3[1,2] = -1im
    g3[2,1] = 1im
    g3[3,4] = -1im
    g3[4,3] = 1im
    return g1,g2,g3
end 
# ========================================================
function matset(ky::Float64)
    hn::Int64 = 4
    H00 = zeros(ComplexF64,4,4)
    H01 = zeros(ComplexF64,4,4)
    g1 = zeros(ComplexF64,4,4)
    g2 = zeros(ComplexF64,4,4)
    g3 = zeros(ComplexF64,4,4)
    #--------------------
    m0::Float64 = 1.5
    tx::Float64 = -1.0
    ty::Float64 = 1.0
    ax::Float64 = 1.0
    ay::Float64 = 1.0
    g1,g2,g3 = Pauli()
    #--------------------
    for m in 1:hn
        for l in 1:hn
            H00[m,l] = (m0-ty*cos(ky))*g1[m,l] + ay*sin(ky)*g3[m,l] 

            H01[m,l] = (-tx*g1[m,l] - 1im*ax*g2[m,l])/2
        end 
    end 
    #------
    return H00,H01
end
# =====================================================
function iteration(omg::Number,ky::Float64)
    hn::Int64 = 4
    eps::Float64 = 1e-8
    err::Float64 = 1.0
    num::Int64 = 0.0
    g0 = zeros(ComplexF64,hn,hn)
    giter = zeros(ComplexF64,hn,hn)
    gdiff = zeros(ComplexF64,hn,hn)
    unit = zeros(ComplexF64,hn,hn)
    h00 = zeros(ComplexF64,hn,hn)
    h01 = zeros(ComplexF64,hn,hn)
    h00,h01 = matset(ky)
    for i in 1:hn
        unit[i,i] = 1
    end
    g0 = inv(omg*unit - h00)
    while(err > eps)
        num += 1
        giter = inv(omg*unit - h00 - h01*g0*transpose(conj(h01))) 
        gdiff = giter - g0
        g0 = giter
        err = abs(sum(gdiff))
    end
    return g0
end
# ===========================================================
function main()
    hn::Int64 = 4
    g0 = zeros(ComplexF64,hn,hn)
    re::ComplexF64 = 0.0
    eta::Float64 = 0.01
    domg::Float64 = 0.01
    dk::Float64 = 0.01
    f1 = open("edgeState.dat","w")
    for omg in -2:domg:2
        for kx in -pi:dk:pi
            g0 = iteration(omg + 1im*eta,kx)
            re = -sum(g0)/pi
            writedlm(f1,[kx/pi omg imag(re)])
        end
    end
    close(f1)
end
# =============================================================
main()
```

## Fortran
```fortran
    module pub
    implicit none
    integer hn,N,itermax
    real eta,dk,de,pi,accuarrcy
    parameter(hn = 4,eta = 0.01,dk = 0.1,de = dk,pi = 3.1415926535,itermax = 100,accuarrcy = 1e-5)
    complex,parameter::im = (0.,1.0)  
    complex H00(hn,hn),H01(hn,hn)
    real one(hn,hn) 
!=================================
    real m0,tx,ty,ax,ay
    complex g1(hn,hn),g2(hn,hn),g3(hn,hn) 
    end module pub
!================= PROGRAM START ============================
    program sol
    use pub
    integer i1
!======parameter value setting =====
    m0 = 1.5
    tx = 1.0
    ty = 1.0
    ax = 1.0
    ay = 1.0
    call main()
    stop 
    end program sol
!=============================================================================================
    subroutine main()
    use pub
    integer i1
    complex GLL(hn,hn),GRR(hn,hn),GBulk(hn,hn)
    real re1,re2,re3,kx,omega
    open(30,file="spectral.dat")
    do kx = -pi,pi,dk
        do omega = -3,3,de
            call surfgreen_1985(omega,kx,GLL,GRR,Gbulk)
            re1 = 0
            re2 = 0
            re3 = 0
            do i1 = 1,hn
                re1 = re1 - aimag(GLL(i1,i1))
                re2 = re2 - aimag(GRR(i1,i1))
                re3 = re3 - aimag(GBulk(i1,i1))
            end do
            re1 = re1/pi
            re2 = re2/pi
            re3 = re3/pi
            write(30,999)kx/pi,omega,re1,re2,re3
        end do
        write(30,*)" "
    end do
    close(30)
999 format(10f11.6)
    return
    end subroutine main
!==================================================
    subroutine surfgreen_1985(omega,ky,GLL,GRR,Gbulk)
    use pub
    real omega,ky
    integer iter
    real real_temp
    complex omegac
    complex GLL(hn,hn),GRR(hn,hn),Gbulk(hn,hn)
    complex alphai(hn,hn),betai(hn,hn),epsiloni(hn,hn),epsilons(hn,hn),epsilons_t(hn,hn)
    complex mat1(hn,hn),mat2(hn,hn),g0(hn,hn)
    !------------------------------------------
    ! call openy(ky)
    call openx(ky)
    epsiloni = H00
    epsilons = H00
    epsilons_t = H00
    alphai = H01
    betai = conjg(transpose(H01))
    omegac = omega + im*eta
    do iter = 1,itermax
        call inv(omegac*one- epsiloni,g0)
        mat1 = matmul(alphai,g0)
        mat2 = matmul(betai,g0)
        g0 = matmul(mat1,betai)
        epsiloni = epsiloni + g0
        epsilons = epsilons + g0
        g0 = matmul(mat2,alphai)
        epsiloni = epsiloni + g0
        epsilons_t = epsilons_t + g0
        g0 = matmul(mat1,alphai)
        alphai = g0
        betai = g0
        real_temp = abs(sum(alphai))
        if (real_temp < accuarrcy) then
            exit
        end if
        call inv(omegac*one - epsilons,GLL)
        call inv(omegac*one - epsilons_t,GRR)
        call inv(omegac*one - epsiloni,GBulk)  
    end do
    return
    end subroutine surfgreen_1985
!====================================================
    subroutine Pauli()
    use pub
    integer i1
    !=== Kinetic energy
    g1(1,1) = 1
    g1(2,2) = -1
    g1(3,3) = 1
    g1(4,4) = -1
    !====== SOC-x
    g2(1,2) = 1
    g2(2,1) = 1
    g2(3,4) = -1
    g2(4,3) = -1
    !====== SOC-y
    g3(1,2) = -im
    g3(2,1) = im
    g3(3,4) = -im
    g3(4,3) = im
    !---------------
    do i1 = 1,hn
        one(i1,i1) = 1  !单位矩阵
    end do
    return
    end subroutine Pauli
!==========================================================
    subroutine openx(ky)
    use pub
    real ky
    integer m,l,k
    call Pauli()
    H00 = 0
    H01 = 0
    do m = 1,hn
        do l = 1,hn
            H00(m,l) = (m0-ty*cos(ky))*g1(m,l) + ay*sin(ky)*g3(m,l) 

            H01(m,l) = (-tx*g1(m,l) - im*ax*g2(m,l))/2
        end do
    end do
    return
    end subroutine openx
!==========================================================
    subroutine openy(kx)
    use pub
    real kx
    integer m,l,k
    call Pauli()
    H00 = 0
    H01 = 0
    do m = 1,hn
        do l = 1,hn
            H00(m,l) = (m0-tx*cos(kx))*g1(m,l) + ax*sin(kx)*g2(m,l)

            H01(m,l) = (-ty*g1(m,l) - im*ay*g3(m,l))/2
        end do
    end do
    return
    end subroutine openy
!=================================================================
    subroutine inv(matin,matout)
    use pub
    complex,intent(in) :: matin(hn,hn)
    complex:: matout(size(matin,1),size(matin,2))
    real:: work2(size(matin,1))            ! work array for LAPACK
    integer::info2,ipiv(size(matin,1))     ! pivot indices
    ! Store A in Ainv to prevent it from being overwritten by LAPACK
    matout = matin
    ! SGETRF computes an LU factorization of a general M-by-N matrix A
    ! using partial pivoting with row interchanges.
    call CGETRF(hn,hn,matout,hn,ipiv,info2)
    if (info2.ne.0)then
      write(*,*)'Matrix is numerically singular!'
      stop
    end if
    ! SGETRI computes the inverse of a matrix using the LU factorization
    ! computed by SGETRF.
    call CGETRI(N,matout,hn,ipiv,work2,hn,info2)
    if (info2.ne.0)then
        write(*,*)'Matrix inversion failed!'
        stop
    end if
    return
    end subroutine inv

```
# 绘图
```shell
set encoding iso_8859_1
#set terminal  postscript enhanced color
#set output 'arc_r.eps'
#set terminal pngcairo truecolor enhanced  font ",50" size 1920, 1680
set terminal png truecolor enhanced font ",50" size 1920, 1680
set output 'density.png'
#set palette defined ( -10 "#194eff", 0 "white", 10 "red" )
set palette defined ( -10 "blue", 0 "white", 10 "red" )
#set palette rgbformulae 33,13,10
unset ztics
unset key
set pm3d
set border lw 6
set size ratio 1
set view map
set xtics
set ytics
#set xlabel "K_1 (1/{\305})"
set xlabel "X_1"
#set ylabel "K_2 (1/{\305})"
set ylabel "Y"
set ylabel offset 1, 0
set colorbox
set xrange [-1:1]
set yrange [-3:3]
set pm3d interpolate 4,4
#splot 'wavenorm.dat' u 1:2:3 w pm3d
#splot 'wavenorm.dat' u 1:2:3 w pm3d
splot 'openy-bhz.dat' u 1:2:3 w pm3d

```

# 参考
1. [Helical edge and surface states in HgTe quantum wells and bulk insulators](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.77.125319)