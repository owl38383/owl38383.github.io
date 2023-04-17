---
layout: default
title: docker-compose 详细内容
parent: 日常问题记录
nav_order: 4
---



### cat docker-compose.yml
``` docker
version: '3.4'
services:
  klvchen:
    image: ${IMAGE_NAME}
    restart: always                     # docker stack 命令启动不支持该参数
    env_file:
      - .env                            # 调用 .env 文件的变量
    environment:
      - JAVA_OPTS=-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5006      # 设置环境变量
    ports:
      - 5006:5006                       # 暴露端口
    extra_hosts:                        # 设置容器 hosts
      - "admin.klvchen.com:192.168.0.200"
    healthcheck:                        # 设置健康检查
      test: ["CMD", "curl", "-f", "http://localhost:8080/actuator/health"]
      interval: 1m30s
      timeout: 10s
      retries: 3
      start_period: 30s
    deploy:
      replicas: 3                       # 指定部署数量
      placement:                        # 指定部署的服务器位置
        constraints:
        - node.hostname == gz01
   depends_on:                          # 指定容器启动顺序依赖
      - elk-elasticsearch
    networks:
      backend-swarm:
        aliases:
        - klvchen
networks:
  backend-swarm:
    external:
      name: backend-swarm
```

### cat .env
```
IMAGE_NAME=ha.klvchen.com/klvchen:2018-12-14_18-25
```
### 官网 docker-compose.yml 参数介绍
[Overview | Docker Documentation](https://docs.docker.com/compose/compose-file/)
