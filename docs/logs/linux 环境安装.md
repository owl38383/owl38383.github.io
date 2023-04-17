---
layout: default
title: linux 环境安装
parent: 日常问题记录
nav_order: 4
---


### 安装jdk1.8

1. 从官网下载 jdk 安装版本包 
```shell
wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn/java/jdk/8u202-b08/1961070e4c9b4e26a04e7f5a083f551e/jdk-8u202-linux-x64.tar.gz
```
```shell
wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://www.oracle.com/webapps/redirect/signon?nexturl=https://download.oracle.com/otn/java/jdk/8u281-b09/89d678f2be164786b292527658ca1605/server-jre-8u281-linux-x64.tar.gz
```
2. 解压压缩到到指定目录
```shell
mv jdk-8u202-linux-x64.tar.gz jdk-8u202-linux-x64.tar
yum install tar
tar -xvf jdk-8u202-linux-x64.tar -C /usr/local/src/
```

3. 设置环境变量

``` shell
echo "export JAVA_HOME=/usr/local/src/jdk1.8.0_161" >> /etc/profile;
echo "export JRE_HOME=${JAVA_HOME}/jre" >> /etc/profile;
echo "export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib" >> /etc/profile;
echo "export  PATH=${JAVA_HOME}/bin:$PATH" >> /etc/profile;
source /etc/profile
```

4. 查看版本
 
```shell
[root@iz2zeeilxaojxvgropeim8z src]# java -version
java version "1.8.0_161"
Java(TM) SE Runtime Environment (build 1.8.0_161-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.161-b12, mixed mode)
```

### 安装 openjdk 
```
yun search jdk

yum install java-***

yum install java-****-devel	
```

### 查看java进程
```
jps
```
### 安装maven 使用mvn 命令
 
1. 官网下载指定版本包
```
wget https://mirrors.bfsu.edu.cn/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
```
2. 解压到指定目录下
```
tar -xvf apache-maven-3.6.3-bin.tar.gz
export PATH=/usr/local/src/apache-maven-3.6.3/bin:$PATH >> /etc/profile;
```
        	
3. 查看版本 mvn -v
```
[root@iz2zeeilxaojxvgropeim8z src]# mvn -v
Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
Maven home: /usr/local/src/apache-maven-3.6.3
Java version: 1.8.0_161, vendor: Oracle Corporation, runtime: /usr/local/src/jdk1.8.0_161/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "linux", version: "3.10.0-514.26.2.el7.x86_64", arch: "amd64", family: "unix"
```
### 安装RocketMQ
1. 从官网下载二进制包到指定目录
```
wget https://mirrors.bfsu.edu.cn/apache/rocketmq/4.8.0/rocketmq-all-4.8.0-bin-release.zip
```
2. 解压文件到指定目录
```
unzip -d /usr/local/src rocketmq-all-4.8.0-bin-release.zip
```
3. 启动服务
    	 
> 启动不起来 调整脚本内存大小
```
#nohup sh bin/mqnamesrv >> /usr/local/logs/rocketmqlogs/mqnamesrv.log 2>&1 &

tail -n 200 -f /usr/local/logs/rocketmqlogs/mqnamesrv.log

#nohup sh bin/mqbroker -n localhost:9876 >/usr/local/logs/rocketmqlogs/broker.log 2>&1 &

ps -elf | grep rocketmq|awk '{print $1}' | xargs kill

nohup sh /usr/local/src/rocketmq/bin/mqbroker -n localhost:9876 >> /usr/local/src/rocketmq/logs/broker.out 2>&1 &
nohup sh /usr/local/src/rocketmq/bin/mqnamesrv >> /usr/local/src/rocketmq/logs/mqnamesrv.out 2>&1 &

nohup java -Xms128m -Xmx256m -Xmn128m \
-jar /usr/local/src/rocketmq/rocketmq-console-ng-2.0.0.jar \
--server.port=9877 \
--rocketmq.config.namesrvAddr=101.200.222.212:9876 \>> /usr/local/src/rocketmq/logs/rocketmq-console.out 2>&1 &
```
### 安装 redis

    
### 安装nacos
1. 官网下载二进制安装文件
```
wget https://hub.fastgit.org/alibaba/nacos/releases/download/1.4.1/nacos-server-1.4.1.tar.gz
```

2. 启动命令(standalone代表着单机模式运行，非集群模式):
```
sh /usr/local/src/nacos/bin/startup.sh -m standalone
```
### 安装 sentinel

* 启动命令

```
nohup java -Xms128m -Xmx256m -Xmn128m \
-Dserver.port=8748 \
-Dcsp.sentinel.dashboard.server=localhost:8748 \
-Dproject.name=sentinel-dashboard \
-jar /usr/local/src/sentinel.jar >> /usr/local/src/logs/sentinel.out 2>&1 &
```

    
> rz 命令安装：  yum install lrzsz
 
		