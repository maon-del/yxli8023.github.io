---
title: 监测程序运行状态并发送邮件
tags: Code Shell Linux
layout: article
license: true
toc: true
key: a20210519
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
这篇博客整理一个脚本,用来在服务器上给自己发邮件,主要结合程序执行监测,在程序执行完毕之后给自己发邮件提醒,可以让自己及时查看结果并进行下一步的计算过着执行别的任务,做这个事情最主要的原因是想节省时间,同时也有自己懒的原因
{:.info}
<!--more-->
在前面[监测程序运行的Shell脚本](https://yxli8023.github.io/2021/05/15/Shell-Monitor.html)这篇博客中,虽然提供了监测程序运行的脚本,但是任务是否执行完毕还是需要自己登录服务器进行查看,这里就想整理一个脚本,在程序执行完毕之后通过邮件方式进行提醒,这样可以让自己及时的查看计算结果并开始下一步的计划,极大的方便了自己,同时也可以节省不少的时间,专心去做别的事情.
```python
import smtplib
from email.mime.text import MIMEText
import sys,os
 
#QQ邮箱提供的SMTP服务器
mail_host = 'smtp.qq.com'
#服务器端口
port = 465
send_by = '********@qq.com' # QQ邮箱账号
password = 'asdfghjkl' # 开启QQ邮箱STMP后获得的一串符号
send_to = 'abcd@mail.com' # 目标邮箱
def send_email(title,content,):
    #创建了MIMEText类，相当于在写邮件内容，是plain类型
      message = MIMEText(content,'plain','utf-8')
      message["From"] = send_by
      message['To'] = send_to
      message['Subject'] = title
      try:
          #注意第三个参数，设置了转码的格式(我不设的时候会报解码错误)
          smpt = smtplib.SMTP_SSL(mail_host, port, 'utf-8')
          smpt.login(send_by,password)
          smpt.sendmail(send_by, send_to,message.as_string())
          print("发送成功")
      except:
          print("发送失败")
def main():
    title = sys.argv[1]  # 接受第一个输入参数
    content = sys.argv[2]  # 接受第二个输入参数
    send_email(title,content)
if __name__ == "__main__":
    main()
```
这里只需要配置好自己要发送邮件的qq邮箱与接受邮件消息的邮箱即可,qq邮箱需要去开启STMP服务,这个可以自行百度解决.配置号邮箱之后,就只需要确定输入参数邮件标题`title`与邮件内容`content`.这里使用了`sys.argv`这个函数,在使用这个python脚本的时候需要输入参数
```shell
python3 filename.py "title" "content"
```
通过这样的执行之后,邮件标题即为**title**,邮件内容为**content**.

# 实例
```shell
#!/bin/sh  
#============ get the file name ===========  
Folder_A=$(pwd) 
for file_a in ${Folder_A}/*.f90
	do 
	if [ -n "$file_a" ];then
		temp_file=`basename $file_a  .f90` 
		ifort -mkl -O3 -CB $file_a -o $temp_file.out 
		if [ -e $temp_file.out ];then
			./$temp_file.out &
		fi
	fi
done
python3 pathToMail/mail.py "Code Complier" "Your Code have been finished"
```
通过这个shell脚本,当文件夹中所有的fortran程序都编译执行完毕之后,就会发送一封邮件到我的邮箱提醒我任务进度.同样也可将这个发送邮件的python脚本和我前面监测程序运行的shell脚本结合,提醒程序执行进度,nice!!!!!
