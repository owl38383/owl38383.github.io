---
layout: default
title: java Web 项目热更新
parent: 日常问题记录
nav_order: 4
---


![image.png](http://halo.mbad.top/upload/2021/07/image-0ea5d1a600c6420bb6b8120e598cd57c.png)

Build 打上勾勾


java 项目自动重启 Springboot
1. pom.xml 增加依赖
	<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
	    <optional>true</optional>
        </dependency>
2. idea 注册表设置
   双击 shift 搜索 Registry...

搜索 running 打上勾勾
![image.png](http://halo.mbad.top/upload/2021/07/image-d64393bf77ed4510b76090df6301e8dd.png)
重启idea 即可
   