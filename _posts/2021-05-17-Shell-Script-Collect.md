---
title: 整理便捷的shell脚本及命令
tags: Code Shell
layout: article
license: true
toc: true
key: a20210517
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
cover: /assets/page-article-header-overlay-background-image-header-background.jpg
author: YuXuan
show_author_profile: true
---
平时在服务器上会用到很多shell命令来进行文件处理等操作,这篇博客主要就是整理我平时学到和用到的方便的shell脚本以及一些方便快捷的命令,方便自己使用的时候进程查阅.
{:.info}
<!--more-->
# 批量kill进程
```shell
#! /bin/bash
com1=$(ps -u yxli|grep out|awk '{print $1}')
#com1=$(ps -u yxli)
for i in $com1
do 
	#echo $i
	kill -9 $i
done
```
从自己(yxli)的进程中(`ps -u yxli`)寻找`out`结尾的进程(`grep out`)并提取第一列的进程号(`awk '{print $1}'`),通过一个`for`循环遍历所有的进程号,然后强制杀死进程(`kill -9 $i`)

这个命令只使用与自己组里的小服务器上使用,如果是服务器集群,或者超算上面,还是乖乖用作业提交脚本和队列系统管理来取消自己提交的错误作业.
{:.success}

# 批量创建文件夹
```shell
for ((i=0;i<=50;i=i+5))do mkdir dir_name$i;done
```
![png](/assets/images/shell/shell1.png)

# 批量复制文件
```shell
for ((i=5;i<=50;i=i+5))do cp bulkimp0.f90 bulkimp$i.f90;done
```
# 批量修改文件内容
```shell
for ((i=0;i<=50;i=i+5))do sed -i "47s/0/$i/g" bulkimp$i.f90;done
```
这个命令会通过循环,将每个文件中第**47行(47s)**的0替换为循环中的**i**.
# 查看用户所有进程
```shell
ps -u yxli
```
这里查询的是用户`yxli`当前所有进程

![png](/assets/images/shell/shell2.png)

```shell
ps|awk '{print $1}'
```
通过通道命令只截取进程ID这一列的内容

![png](/assets/images/shell/shell3.png)

同样可以查询某个用户特定名称的进程,即前面所示的`CMD`这一列中满足特定名称的进程
```shell
ps -u yxli|grep out|awk '{print $1}'
```
这一行可以提取用户`yxli`进程名中包含`out`的所有进程的ID号,如果进程有问题,可以通过前面的批量操作来将所有的进程一次性kill.

# vasp删除多余文件
```shell
rm CHG IBZKPT DOSCAR O* XDATCAR WAVECAR noh* vasprun.xml EIGENVAL REPORT PCDAT PROCAR C*
```
vasp主要的文件只有4个,有时候我们想删除其他的文件,可以用上面的命令,可将其写成脚本,然后再.bashrc中通过一个简单的命令来执行这个操作.

# vasp运行
```shell
alias v5='nohup mpirun -np 10 v5_gam &'
alias v5s='nohup mpirun -np 10 v5_ncl&'
```
开启10个核来执行vasp

# 文件大小显示
```shell
alias ll='ls --block-size=M -l -t'
```
以`M`为单位显示文件大小.
