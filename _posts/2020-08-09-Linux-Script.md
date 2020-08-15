---
title: Linux中批量执行编译并运行Fortran
tags: Linux Fortran Shell
layout: article
license: true
toc: true
pageview: true
aside:
    toc: true
sitemap: true
mathjax: true
author: YuXuan
show_author_profile: true
---
最近因为要大量重复的跑一些程序，而且只是参数的小修，所以干脆花点时间整理一个界几个shell脚本，来自动的完成程序的编译及执行。
<!--more-->
# 批量编译Fortran并运行
```shell
#!/bin/sh  
#============ get the file name ===========  
Folder_A=$(pwd)  	#要批量编译当前文件夹下面的Fortran
for file_name in ${Folder}/*.f90
do 
	temp_file=`basename $file_name  .f90` 
	ifort -mkl $file_name -o $temp_file.out 
	./$temp_file.out &   # 编译成功之后自动运行
done
rm *out   # 删除编译后文件
```
# 递归的读取指定文件夹下面的所有Fortran文件并编译执行
```shell
#!/bin/bash 
function getdir(){
    for element in `ls $1`
      do
        dir_or_file=$1"/"$element
    if [ -d $dir_or_file ]
      then
        getdir $dir_or_file
      else  # 下面的全是文件
	  	if [ "${dir_or_file##*.}"x = "f90"x ]||[ "${dir_or_file##*.}"x = "f"x ];then	# 筛选处特定后缀的文件
    		dir_name=`dirname $dir_or_file` # 读取目录
			file_name=`basename $dir_or_file .f90` # 读取以f90结尾的文件名
			out_file_name="$dir_name/$file_name"  # 定义编号成功的文件名称
			ifort -mkl $dir_or_file -o $out_file_name.out  # 编译后文件名以out结尾
			dir1=`dirname $out_file_name`  # 读取编译成功文件的路径,只提取目录
			cd $dir1  # 切换到具体的文件夹
			./$file_name.out 1>mes 2>bad &  # 执行该文件夹下面编译好的文件，后缀名为out
			# ./$out_file_name.out 1>mes 2>bad &
			# rm $out_file_name.out
		fi
    fi
done
}
 
root_dir=$(pwd) 
getdir $root_dir
```
# 批量复制文件并修改文件内容
```shell
for ((i=0;i<=30;i=i+5)); do cp bulkimp.f90 bulkimp$i.f90;done #批量复制文件并以$i的值重命名
for ((i=0;i<=30;i=i+5)); do sed -i "47s/30/$i/g" bulkimp$i.f90;done #批量修改文件内容(将第47行的30替换成$i的值)
```
# 批量杀死进程
```shell
ps -ef | grep out | grep -v grep | awk '{print "kill -9 "$2}'|sh  #批量杀死进程名后缀为out的进程
```
# 一些自己定义的Linux命令
```shell
alias ps='ps -u yxli'   # 查看自己所有进程
alias proid='ps|grep *.out'  #查看以out结尾的进程(正好可以配合前面批量编译Fortran来使用)
```