---
title: VASP输出文件内容结构解析(未完成)
tags: vasp
layout: article
license: true
toc: true
key: a20210806
#cover: /assets/images/GroupTheory/cube_symmetry.jpg
header:
  theme: dark
  background: 'linear-gradient(135deg, rgb(34, 139, 87), rgb(139, 34, 139))'
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
pageview: true
sitemap: true
mathjax: true
author: YuXuan
show_author_profile: true
---
这里整理一下最近学习vasp的时候,对一些输出文件中的内容进行一下整理,这样可以让自己再可视化结果的时候,明白需要从哪个文件中寻找什么结果.
{:.info}
<!--more-->
# EIGENVAL
这个文件中会输出对应$k$点的本征值,如果在`KPOINTS`中设置了高对称路径,那么就可以从这个数据文件中得到能带图,其数据内容如下

![png](/assets/images/vasp/eig-1.png)

第一行，前三个整数无意义,第四个整数,如果是2,表示是自旋极化的计算,如果是1,表示非自旋极化的计算.

第2至5行的数据含义不大明确,可以不关心.

第6行的数据表示:第一个数表示体系总的价电子数目,第二个数表示的计算能带时总的$k$点数目,第三个数表示的是计算能带时计算了多少条能带.电子数可以通过在设置`POSCAR`中的原子自己算出来,而$k$点的数目也与在`KPOINTS`中的设置是有关系的,最后的能带数同样可以从`OUTCAR`中的到
```shell
cat OUTCAR | grep NBANDS
```

第8行的前三个数是$k$点的坐标,第四个数是相应$k$点的权重.

第9行给出的是该$k$点对应的本征值的序号(即第几条能带),及相应的本征值.

在知道了这个文件中内容结构之后,就可以通过脚本来提取数据绘制能带图.利用下面的程序进行处理
```shell
    program prog
    real, allocatable :: e(:,:),eup(:,:),edn(:,:)
    real, allocatable :: k(:,:)
    real, dimension(3) ::k0,a
    real, dimension(6) ::xxxx
    character(len = 32):: xx, yy
    write(6,*) 'fermi level (eV)'
    read(5,*) ef
    open(10,file = 'EIGENVAL', status = 'old')
    open(11,file = 'band_fermi.dat')
    open(13,file = 'band.dat')
    read(10,*) iii, iii, iii, ispin  ! 第一行数据读取
    read(10,*) (xxxx(i),i = 1,5) ! 第二行数据读取
    read(10,*) xxxx(6) ! 第三行数据读取
    read(10,*) xx ! 第四行数据读取
    read(10,*) yy ! 第五行数据读取
    read(10,*) nn,nk,nbands  ! 第六行数据读取
    allocate(e(nk,nbands))
    allocate(k(nk,3))
    if(ispin.eq.2) then ! 2表示自旋极化计算
        do i = 1,nk
            read(10,*)
            read(10,*) (k(i,j),j = 1,3),wtk  ! 读取k点坐标及权重
            do j = 1,nbands  ! 读取确定k点下面的每条能带对应的本征值,这里分别是spin-up与spin-down
                read(10,*)jj,eup(i,j),edn(i,j)
            end do
            write(13,9030) (eup(i,j),j = 1,nbands)
            write(14,9030) (edn(i,j),j = 1,nbands)
        end do
        write(6,*)(k(i,j),j = 1,3)
        read(10,*) (e(i,n),n = 1,nbands)
        write(13,9030) (e(i,n),n = 1,nbands)
    else  ! 非自旋极化能带
        do i = 1,nk
            read(10,*)
            read(10,*) (k(i,j),j = 1,3),wtk
            do j = 1,nbands
                read(10,*) jj,e(i,j)  ! 读取能带k点和对应本征值
            end do
            write(13,9030) (e(i,j),j = 1,nbands)
        end do
    end if
9030 format (8f9.5)
    do j = 1,nbands
        dk = 0
        do i = 1,nk
            if (i.eq.1) then
                k0 = k(i,:)
            end if
            a = k(i,:) - k0
            dk = dk + sqrt(dot_product(a,a))
            if(ispin.eq.2) then
                write(11,*)dk,eup(i,j)-ef, edn(i,j)-ef
            else
                write(11,*)dk,e(i,j)-ef
            end if
            k0 = k(i,:)
        end do
        write(11,*)
    end do
    stop
    end program prog
```
在程序运行的时候会要求输入费米能,同样可以在`OUTCAR`中得到
```shell
cat OUTCAR |grep fermi
```
最终可以得到`band_fermi.dat`这个文件,就可以用来绘图了,利用`gnuplot`绘图的脚本如下
```shell
set encoding iso_8859_1
#set terminal  postscript enhanced color font "TimesNewRoman, 11" size 5, 4
set terminal  pngcairo truecolor enhanced lw 5.0 font "TimesNewRoman, 44" size 1920, 1680
set palette rgbformulae 22, 13, -31
# # set palette rgbformulae 7,5,15
set output 'band.png'
set border
# unset colorbox
#set title "C\\_pz" offset 0, -0.8 font "TimesNewRoman, 54"
set style data linespoints
unset ztics
unset key
# # set key outside top vertical center
# # set pointsize 0.3
set view 0,0
set xtics font "TimesNewRoman, 44"
set xtics offset 0, 0.3
set ytics font "TimesNewRoman, 44"
set ytics -10, 5, 10
set ylabel font "TimesNewRoman, 48"
set ylabel offset 1.0, 0
#set xrange [0:5.4704]
set ylabel "Energy (eV)"
set yrange [-8:8]
#set xtics ("G" 0.00000, "K" 1.695, "M" 3.938, "G" 5.407)
#plot 'BAND.dat' u 1:2 w lines lw 1.5 lc 'blue'
plot 'band_fermi.dat' u 1:2 w lines lw 1.5 lc 'blue'
```

![png](/assets/images/vasp/eig-1-band.png)

其实在上面的`EIGENVAL`的数据处理脚本中,同时也包括了自旋极化的处理,因为我暂时并不会计算自旋极化的情况,所以就不对这部分内容进行过多的解读了,之后慢慢的学习,会将这里进行补充.
{:.warning}

# DOSCAR
这个文件中存储的是能带对应的态密度的图,结构如下

![png](/assets/images/vasp/dos-1.png)

其中前5行没什么具体的含义,可以不用关心,第6行前两个数据表示能量范围,第三个数据表示带数,它与`INCAR`中设置的`NEDOS=2001`是相同的,第四个表示费米能.从第7行开始,第一例表示能带,第二列表示对应的态密度,第三列则是积分态密度.这里想要提取的是从第7行开始到第`6+NEDOS`行中的前两列数据,因为在`INCAR`中设置了`NEDOS=2001`,而第2007行后面的数据不是我们想要的,其格式如下

![png](/assets/images/vasp/dos-2.png)

在数据提取出来之后,还要从能量上减去费米能才可以,利用一个脚本
```shell
a=`head -6 DOSCAR|tail -1|awk '{print $3}'` # 从DOSCAR中获取NEDOS的值
b=$((a + 6))    # 确定最后的行数
f=`awk '{if(NR==6)print $4}' DOSCAR`  # 从DOSCAR中获取费米能
sed -n '7,'$b' p' DOSCAR > DOS.dat  # 获取dos数据
awk '{print $1-'$f',$2}' DOS.dat > DOS-final.dat  # 减去费米能
```
得到数据之后就可以利用gnuplot进行态密度绘制
```shell
set encoding iso_8859_1
#set terminal  postscript enhanced color font "TimesNewRoman, 11" size 5, 4
set terminal  pngcairo truecolor enhanced lw 5.0 font "TimesNewRoman, 44" size 1920, 1680
set palette rgbformulae 22, 13, -31
# # set palette rgbformulae 7,5,15
set output 'dos.png'
set border
# unset colorbox
#set title "C\\_pz" offset 0, -0.8 font "TimesNewRoman, 54"
set style data linespoints
unset ztics
unset key
# # set key outside top vertical center
# # set pointsize 0.3
set view 0,0
set xtics font "TimesNewRoman, 44"
set xtics offset 0, 0.3
set ytics font "TimesNewRoman, 44"
#set ytics -10, 5, 10
set ylabel font "TimesNewRoman, 48"
set ylabel offset 1.0, 0
#set xrange [0:5.4704]
#set ylabel "Energy (eV)"
#set yrange [-8:8]
#set xtics ("G" 0.00000, "K" 1.695, "M" 3.938, "G" 5.407)
plot 'DOS-final.dat' u 1:2 w lines lw 1.5 lc 'blue'
```

![png](/assets/images/vasp/dos-3.png)

# 代码下载
上面的用到的代码可以[点击这里下载](/assets/data/vasp-script.zip)

