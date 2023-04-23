---
layout: default
title: Docker 快速安装
createDate: 2023-04-23 08:43
LastModifDate: 2023-04-23 12:59
profileName: aquiver
parent: 代码编程
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
```shell
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

### 安装docker(官方)
``` shell
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

### 安装docker-compose(官方)
```shell
curl -SL https://ghproxy.com/https://github.com/docker/compose/releases/download/v2.17.2/docker-compose-linux-x86_64 -o usr/local/bin/docker-compose
```

###  开源一键安装脚本支持多个源安装

``` shell
bash <(curl -sSL https://gitee.com/SuperManito/LinuxMirrors/raw/main/DockerInstallation.sh)
```