---
title: 利用格林函数求解边界态-快速算法
tags: Code Method Julia Topology
layout: article
license: true
toc: true
key: a20210208
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
前面的一篇博客利用表面格林函数计算了边界态,虽然相比于通常对角化哈密顿量矩阵的方法要节省之间,但是迭代的收敛速度会比较慢,这里就提供一种收敛速度更快的方法来计算边界态.
<!--more-->
在之前的[利用格林函数求解边界态](https://yxli8023.github.io/2021/02/07/EdgeState-GF.html)这篇博客中,利用边界格林函数的方法计算了边界态,但是这个算法的收敛速度会比较慢,这里就提供一个收敛速度更快的方案来计算边界态.关于这个算法的内容可以参考[Highly convergent schemes for the calculation of bulk and surface Green functions](https://iopscience.iop.org/article/10.1088/0305-4608/15/4/009)这篇文章,里面有对算法详细的描述.

# 模型方法
这里选用BHZ模型

$$H(\mathbf{k})=(m_0-t_x\cos k_x-t_y\cos k_y)\sigma_z+\lambda_x\sin k_x\sigma_xs_z+\lambda_y\sin k_y\sigma_y\label{ham}$$

至于具体的计算方法可以阅读[Highly convergent schemes for the calculation of bulk and surface Green functions](https://iopscience.iop.org/article/10.1088/0305-4608/15/4/009)这篇文章。


结果如下图

![png](/assets/images/Julia/edge-gf-2.png)

这里的结果稍稍有点问题,我自己也没有非常明白问题的来源,因为始终没有边界态的出现,而且结果与计算中$k,\omega$的选取间隔有关,与收敛的精度控制也有关系.
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
    tx::Float64 = 1.0
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
# ====================================================================================
function surfgreen_1985(omg::Float64,ky::Float64)
    hn::Int64 = 4
    GLL = zeros(ComplexF64,hn,hn)
    GRR = zeros(ComplexF64,hn,hn)
    GBulk = zeros(ComplexF64,hn,hn)
    iter::Int64 = 0
    itermax::Int64 = 100
    accuarrcy::Float64 = 1E-7
    real_temp::Float64 = 0.0
    omegac::ComplexF64 = 0.0
    eta::Float64 = 0.01
    #-----------------------------------
    alphai = zeros(ComplexF64,hn,hn)
    betai = zeros(ComplexF64,hn,hn)
    epsiloni = zeros(ComplexF64,hn,hn)
    epsilons = zeros(ComplexF64,hn,hn)
    epsilons_t = zeros(ComplexF64,hn,hn)
    mat1 = zeros(ComplexF64,hn,hn)
    mat2 = zeros(ComplexF64,hn,hn)
    g0 = zeros(ComplexF64,hn,hn)
    unit = zeros(ComplexF64,hn,hn)
    #------------------------------------
    H00,H01 = matset(ky)
    epsiloni = H00
    epsilons = H00
    epsilons_t = H00
    alphai = H01
    betai = conj(transpose(H01))
    #-------------------------------------
    for i in 1:hn
        unit[i,i] = 1
    end
    #-------------------------------------
    omegac = omg + 1im*eta
    for iter in 1:itermax
        g0 = inv(omegac*unit- epsiloni)
        mat1 = alphai*g0
        mat2 = betai*g0
        g0 = mat1*betai
        epsiloni = epsiloni + g0
        epsilons = epsilons + g0
        g0 = mat2*alphai
        epsiloni= epsiloni + g0
        epsilons_t = epsilons_t+ g0
        g0 = mat1*alphai
        alphai = g0
        betai = g0
        real_temp = abs(sum(alphai))
        if real_temp < accuarrcy
            break
        end
    end
    GLL = inv(omegac*unit - epsilons)
    GRR = inv(omegac*unit - epsilons_t)
    GBulk = inv(omegac*unit - epsiloni)
    return GLL,GRR,GBulk
end
# ==========================================================
function surfState()
    hn::Int64 = 4
    dk::Float64 = 0.01
    domg::Float64 = 0.05
    ky::Float64 = 0.0
    omg::Float64 = 0.0
    GLL = zeros(ComplexF64,hn,hn)
    GRR = zeros(ComplexF64,hn,hn)
    GBulk = zeros(ComplexF64,hn,hn)
    f1 = open("edgeState.dat","w")
    for ky in -pi:dk:pi
        for omg in -3:domg:3
            GLL,GRR,GBulk = surfgreen_1985(omg,ky)
            re1 = -imag(sum(GLL))/pi
            re2 = -imag(sum(GRR))/pi
            re3 = -imag(sum(GBulk))/pi
            writedlm(f1,[ky/pi omg re1 re2 re3])
        end
    end
    close(f1)
end
# =========================================================
@time surfState()
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
1. [Highly convergent schemes for the calculation of bulk and surface Green functions](https://iopscience.iop.org/article/10.1088/0305-4608/15/4/009)