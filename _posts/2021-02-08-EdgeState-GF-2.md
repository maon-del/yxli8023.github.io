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

# 参考
1. [Highly convergent schemes for the calculation of bulk and surface Green functions](https://iopscience.iop.org/article/10.1088/0305-4608/15/4/009)