---
layout: default
title: docker 安装和清理
createDate: 2023-04-03 08:55
LastModifDate: 2023-04-23 13:10
profileName: aquiver
parent: 代码编程
nav_order: 4
---

## docker 环境安装
[Docker 快速安装](日常问题记录/代码编程/Docker%20快速安装.md)


### 一、docker-compose介绍 
- [docker compose 停止]( https://blog.csdn.net/weixin_42576410/article/details/113582029)<br>
- [docker清理缓存](https://blog.csdn.net/weixin_47284857/article/details/123876032)

### 二、docker清理
* 删除所有已经停止的容器 <br>注意：要先确认停止的容器中是否有不可以删除的，也可以删除后使用镜像再启一个容器。  
```shell
docker rm $(docker ps -a|grep Exited |awk '{print $1}')
docker rm $(docker ps -qf status=exited)
```
* 删除所有未打标签的镜像   
```shell
docker rmi $(docker images -q -f dangling=true)
```
* 删除所有无用的volume  
```shell
docker volume rm $(docker volume ls -qf dangling=true)
```

* 清理磁盘、删除关闭的容器、无用的数据卷和网络参数： -a : 清除所有没有容器引用的镜像时，使用 
```shell
docker system prune -a -f 
```    
* 强制清除,不会出现提示,使用
```shell
docker system prune -f
```         
* 用来限制要保留的镜像的范围，例如：只清除超过创建时间超过24小时的镜像
```shell
docker image prune -a --filter "until=24h"
```


### 三、docker命令扩展
* 停止所有运行中的容器   

```shell
docker stop $(docker ps -q)
```

* 停止所有容器   

```shell
docker stop $(docker ps -a -q)
```

* 重启所有容器   

```shell
docker restart $(docker ps -a -q)
```

* 获取停止的容器id   

```shell
cut：
docker ps -a | grep Exited | cut -d' ' -f1
 
awk：
docker ps -a | grep Exited | awk '{print $1}'

```

* 启动所有停止的容器   

```shell
docker ps -a | grep Exited | awk '{print $1}' |xargs docker start
```

* 删除所有容器   

```shell
docker rm $(docker ps -aq)
```

* 删除所有镜像  
 
```shell
docker rmi $(docker images -q)
```
### 四、清理docker缓存脚本

``` bash
#!/bin/sh 

echo "======== start clean docker containers logs ========"  

logs=$(find /var/lib/docker/containers/ -name *-json.log)  

for log in $logs
    do
	echo "clean logs : $log"
	cat /dev/null > $log 
    done

echo "======== end clean docker containers logs ========" 


```
###  五、docker国内仓库配置
```shell
cd /etc/docker
vim daemon.json
{
    "registry-mirrors": [
        "https://dockerproxy.com",
        "https://1nj0zren.mirror.aliyuncs.com",
        "https://docker.mirrors.ustc.edu.cn",
        "http://f1361db2.m.daocloud.io",
        "https://dockerhub.azk8s.cn"
    ]
} 
systemctl daemon-reload 
systemctl restart docker.service
docker info
```



### docker volume 命令
```shell
docker volume create xxx：创建卷名  
docker volume inspect xxx：查询卷详情  
docker volume ls: 列出所有卷  
docker volume prune: 移除无用卷
```

### 卸载docker
``` shell
sudo yum remove docker \
		docker-client \
		docker-client-latest \
		docker-common \
		docker-latest \
		docker-latest-logrotate \
		docker-logrotate \
		docker-engine
sudo yum remove docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

### docker镜像相关命令
```shell
docker images 
docker search ***
docker pull ***:latest
docker rmi <imageId>
```
#### 删除 none 奖项
```shell
docker rmi $(docker images -f "dangling=true" -q)
```
#### 查看docker环境变量	
```shell
docker inspect <启动容器名>
```
#### 查看docker 启动情况
```shell
docker ps -a
docker logf <启动容器名>
```
#### 运行容器
``` shell
docker run 
-d <imageId>
-it
-v
-p
--name
```

#### docker-compose 相关命令
在文件目录下执行 默认是读取docker-compose.yml/docker-compose.yaml 文件执行
- 后台运行
```shell
docker-compose up -d
```
- 停止运行
```shell
docker-compose stop
```
- 停止并删除容器 
```shell
docker-compose down 
```
