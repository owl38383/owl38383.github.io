---
layout: default
title: Java Web 项目热更新
createDate: 2023-04-23 08:43
LastModifDate: 2023-04-23 13:16
profileName: aquiver
parent: 代码编程
nav_order: 4
---

## java 项目自动重启 Springboot
1. pom.xml 增加依赖
``` xml
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-devtools</artifactId>
		<optional>true</optional>
	</dependency>
```

2. idea 注册表设置
   > 双击 shift 搜索 Registry...
   >>搜索 running 打上勾勾

3. 重启idea 即可
   
