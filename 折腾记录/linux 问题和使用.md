---
layout: default
title: linux 问题和使用
createDate: 2022-12-27 09:01
LastModifDate: 2023-04-17 16:25
profileName: aquiver
parent: 折腾记录
nav_order: 4
---

### centos vim 中文乱码
```
vim ~/.vimrc
set fileencodings=utf-8,gb2312,gb18030,gbk,ucs-bom,cp936,latin1
set enc=utf8
set fencs=utf8,gbk,gb2312,gb18030
```

### 杀死相关进程
```
ps -ef | grep harvester | grep -v grep | cut -c 9-15 | xargs kill -s 9
```

```
ps aux|grep sync_alarm_data|awk '{print $2}'|xargs kill -9
```


### nohup和screen 使用

    screen -S cxn ：创建一个进程，后缀名为cxn
    screen -ls ：查看所有进程
    screen -r 进程号：进入一个进程
    kill -9 进程号：杀死进程
    screen -wipe：移除死掉的进程
    ctrl+a，再按d即可挂起

### 下载指令
1. 指令一

```
wget --debug --header="User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36 Edg/91.0.864.59" https://zf.sc.chinaz.com/Files/DownLoad/font/xmfont3616efn.rar
```
1. 指令二
    
```
wget --no-check-certificate -qO client-linux.py 'https://raw.githubusercontent.com/cppla/ServerStatus/master/clients/client-linux.py'
```


### 查看端口使用情况
1. 查看端口使用情况

```
iptables -nL
```
1. 查看端口占用

```
lsof -i:80
```

### 服务器之间复制文件

```
scp root@192.168.8.61:/opt/fubang  ./
```
   
### 查看所有系统服务

```
systemctl list-units --type=service
```

### 替换yum 源

1. 进入 yum 源配置目录   

    `cd /etc/yum.repos.d`

2. 备份原 yum 源基础配置文件
     
    `mv CentOS-Base.repo CentOS-Base.repo.bak`

3. 切换 yum 基础源至阿里源      

    `wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo`

4. 清空缓存    
  
   ` yum clean all && yum makecache`


### 配置系统代理 这种方式只在当前窗口生效

1. 本机代理

```	
vim /etc/profile

export proxy="http://127.0.0.1:10809"     
export http_proxy=$proxy        
export https_proxy=$proxy       
export ftp_proxy=$proxy     
export no_proxy="localhost, 127.0.0.1, ::1" 

source /etc/profile
```

2. docker 容器代理 （写入到 `/etc/profile` 或 `/etc/environment` 文件中）

```
vim /etc/profile

export proxy="http://172.17.0.1:10809"     
export http_proxy=$proxy        
export https_proxy=$proxy       
export ftp_proxy=$proxy     
export no_proxy="localhost, 127.0.0.1, ::1"   

source /etc/profile
```

3. 局域网代理

```
vim /etc/profile

export proxy="http://192.168.8.10:10809"       
export http_proxy=$proxy        
export https_proxy=$proxy       
export ftp_proxy=$proxy     
export no_proxy="localhost, 127.0.0.1, ::1"   

source /etc/profile
```


### 查找并替换

1. 查看包含118.190.73.218内容的文件

```
find ./ -type f -regex ".*\.xml\|.*\.js.*\|.*\.properties" | xargs grep "118.190.73.218"
```

2. 查找完成后进行替换为old_text为new_text 

```
find ./ -type f -regex ".*\.xml\|.*\.js.*\|.*\.properties" | xargs perl -pi -e"s/old_text/new_text/g"
```

3. 查找完成后进行替换为old_text为new_text
```
find /home/user/documents -type f -exec sed -i 's/old_text/new_text/g' {} +
```

4. 内容替换 单个文件
```
sed -i 's/old_text/new_text/g' file.txt
```

### unzip 解压乱码
```
unzip -O GBK xxx.zip -b 路径
```


### 脚本地址
* https://cdn.jsdelivr.net/gh/owl38383/cdn.io@main//shell/clear_linux_cache.sh
* https://cdn.jsdelivr.net/gh/owl38383/cdn.io@main//shell/install_jdk_1.8.sh
* https://cdn.jsdelivr.net/gh/owl38383/cdn.io@main//shell/install_latest_jdk.sh
* https://cdn.jsdelivr.net/gh/owl38383/cdn.io@main/shell/install_latest_nginx.sh
* https://cdn.jsdelivr.net/gh/owl38383/cdn.io@main/shell/install_latest_nodejs.sh
* https://cdn.jsdelivr.net/gh/owl38383/cdn.io@main/shell/port_script.sh
* https://cdn.jsdelivr.net/gh/owl38383/cdn.io@main/shell/start.sh
* https://cdn.jsdelivr.net/gh/owl38383/cdn.io@main/shell/stop.sh
* https://cdn.jsdelivr.net/gh/owl38383/cdn.io@main/shell/switch_to_aliyun_yum.sh
* https://cdn.jsdelivr.net/gh/owl38383/cdn.io@main/shell/uninstall_docker_centos.sh
* https://cdn.jsdelivr.net/gh/owl38383/cdn.io@main/shell/uninstall_docker_debian.sh
* https://cdn.jsdelivr.net/gh/owl38383/cdn.io@main/shell/upgrade_python_to_2.7.8.sh