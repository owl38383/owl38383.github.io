---
layout: default
title: mysql 故障排查
createDate: 2022-11-23 17:02
LastModifDate: 2023-03-17 14:16
profileName: aquiver
parent: 折腾记录
nav_order: 4
---

## 查看最大连接数
show variables like '%max_connections%';
## 查看占用连接
show processlist;
## 设置最大连接数
set GLOBAL max_connections=6000;

## 查看当前连接状态
show status like '%Threads%';
>[!INFO]
>命令：show status like '%下面变量%';
 
| 命令                     | 描述                                                     |
| ------------------------ | -------------------------------------------------------- |
| Aborted_clients          | 由于客户没有正确关闭连接已经死掉，已经放弃的连接数量。   |
| Aborted_connects         | 尝试已经失败的MySQL服务器的连接的次数。                  |
| Connections              | 试图连接MySQL服务器的次数。                              |
| Created_tmp_tables       | 当执行语句时，已经被创造了的隐含临时表的数量。           |
| Delayed_insert_threads   | 正在使用的延迟插入处理器线程的数量。                     |
| Delayed_writes           | 用INSERT DELAYED写入的行数。                             |
| Delayed_errors           | 用INSERT DELAYED写入的发生某些错误(可能重复键值)的行数。 |
| Flush_commands           | 执行FLUSH命令的次数。                                    |
| Handler_delete           | 请求从一张表中删除行的次数。                             |
| Handler_read_first       | 请求读入表中第一行的次数。                               |
| Handler_read_key         | 请求数字基于键读行。                                     |
| Handler_read_next        | 请求读入基于一个键的一行的次数。                         |
| Handler_read_rnd         | 请求读入基于一个固定位置的一行的次数。                   |
| Handler_update           | 请求更新表中一行的次数。                                 |
| Handler_write            | 请求向表中插入一行的次数。                               |
| Key_blocks_used          | 用于关键字缓存的块的数量。                               |
| Key_read_requests        | 请求从缓存读入一个键值的次数。                           |
| Key_reads                | 从磁盘物理读入一个键值的次数。                           |
| Key_write_requests       | 请求将一个关键字块写入缓存次数。                         |
| Key_writes               | 将一个键值块物理写入磁盘的次数。                         |
| Max_used_connections     | 同时使用的连接的最大数目。                               |
| Not_flushed_key_blocks   | 在键缓存中已经改变但是还没被清空到磁盘上的键块。         |
| Not_flushed_delayed_rows | 在INSERT DELAY队列中等待写入的行的数量。                 |
| Open_tables              | 打开表的数量。                                           |
| Open_files               | 打开文件的数量。                                         |
| Open_streams             | 打开流的数量(主要用于日志记载）                          |
| Opened_tables            | 已经打开的表的数量。                                     |
| Questions                | 发往服务器的查询的数量。                                 |
| Slow_queries             | 要花超过long_query_time时间的查询数量。                  |
| Threads_connected        | 当前打开的连接的数量。                                   |
| Threads_running          | 不在睡眠的线程数量。                                     |
| Uptime                   | 服务器工作了多少秒。                                     |


```
select  host, user, authentication_string, plugin from mysql.user;

use mysql;

update user set host = '%' where user = 'root';

FLUSH PRIVILEGES;
```


### 更改替换字段部分内容

```
UPDATE info_app SET navigation=replace(navigation,'jcloud.fubangyun.com','192.168.8.118')

```

# 数据库同步服务

```
show master logs;
show master status;
```

## 查看日志详情
```
show binlog events in 'mysql-bin.000036'
show grants for 'canal' 
```
## 查看bing-log 日志模式
```
show variables like 'log_bin';
show variables like 'binlog_format';
show variables like '%server_id%';
```
## 配置 binlog-format 为 ROW 模式,my.cnf 中配置如下
```
[mysqld]
log-bin=mysql-bin # 开启 binlog
binlog-format=ROW # 选择 ROW 模式
server_id=1 # 配置 MySQL replaction 需要定义，不要和 canal 的 slaveId 重复
```
## 查看是否有slave 权限用户
```
show grants for 'canal' 
```
## 创建slave权限用户
```
CREATE USER canal IDENTIFIED BY 'canal';  
GRANT SELECT, REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'canal'@'%';
-- GRANT ALL PRIVILEGES ON *.* TO 'canal'@'%' ;
FLUSH PRIVILEGES;
```
## 查看mysql-bin 文件名
```
show master logs;
```
## 查看日志文件定位
```
show master status;
```


## 启动deployer 本地配置
```
sh bin/stop.sh local
rm -rf conf/dev_3306
sh bin/startup.sh local


sh bin/stop.sh 
sh bin/startup.sh 
```
oneinstack