---
layout: default
title: Centos 安装远程桌面
parent: 日常问题记录
nav_order: 4
---



# 安装远程桌面服务器软件包
`sudo apt-get install xrdp`

# 启动远程桌面服务
`sudo systemctl start xrdp`

# 设置远程桌面服务为开机启动
`sudo systemctl enable xrdp`

https://www.cnblogs.com/xinbigworld/p/16077982.html
