---
layout: default
title: Docker 使用mysqldump 备份数据库 加入linux定时之后失败问题
parent: 日常问题记录
nav_order: 4
---


### 问题描述
- mysql是docker方式部署，使用docker exec -it 容器名 mysqldump …命令，并加入到linux自动任务来备份mysql数据库失败
- 具体表现
- ![image.png](https://file.mbad.top/file/202304171210652.png)
### 解决方法
- 经分析docker加入了-t参数导致，加入-t是开启了一个伪终端，crontab自动任务执行时是进入了一个伪终端里进行备份，所以会导致备份失败。