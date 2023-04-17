---
layout: default
title: Nginx反代之后网站ws协议无法连接问题
parent: 日常问题记录
nav_order: 4
---


### 完整配置 
```
proxy_pass http://127.0.0.1:3000; // 代理到本地3000端口
proxy_set_header Host $http_host; // 设置 Host header 为客户端请求头中的 Host
proxy_set_header X-Real-IP $remote_addr; //设置 X-Real-IP header 为客户端真实 IP
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; // 设置 X-Forwarded-For header 为经过的代理 IP 列表
proxy_set_header X-Forwarded-Proto $scheme; // 设置 X-Forwarded-Proto header 为客户端请求协议
proxy_set_header X-Forwarded-Port $server_port; // 设置 X-Forwarded-Port header 为服务器端口
proxy_set_header REMOTE-HOST $remote_addr;// 设置 REMOTE-HOST header 为客户端真实 IP
proxy_set_header Upgrade $http_upgrade;// 设置协议升级头，支持 WebSockets
proxy_set_header Connection $connection_upgrade;//设置连接头，支持 WebSockets
proxy_http_version 1.1;// 设置代理协议版本
```