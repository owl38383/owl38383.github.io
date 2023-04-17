---
layout: default
title: Docker 快速安装
parent: 日常问题记录
nav_order: 4
---


### Docker安装
1. docker 一键安装
    
```shell
sudo curl -sSL https://get.daocloud.io/docker | sh
```
2. docker-compose 编排工具安装
 
```shell
sudo curl -L https://ghproxy.com/https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
3. 同步docker容器时区和时间 
```
-v /etc/timezone:/etc/timezone:ro \
-v /etc/localtime:/etc/localtime:ro \
```
4. docker 相关命令
```shell
systemctl enable docker # 开启开机自启动
systemctl start docker #启动docker
systemctl stop docker 停止docker 
systemctl restart docker # 重启docker

service docker start
service docker stop
service docker restart

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
``` docker
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
```
docker-compose up -d
```
- 停止运行
```
docker-compose stop
```
- 停止并删除容器 
```
docker-compose down 
```