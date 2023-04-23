---
layout: default
title: Linux 使用shell命令增加定时任务
createDate: 2023-04-23 08:43
LastModifDate: 2023-04-23 13:03
profileName: aquiver
parent: 代码编程
nav_order: 4
---


### 无需root权限
```shell
crontab -l > conf && echo "0 1 * * * $DIR/backupDockerDB.sh ${input_ports[@]}" >> conf && crontab conf && rm -f conf
```

> [!INFO]
>这个命令的作用是将当前用户的 crontab 文件内容导出到 conf 文件，然后在 conf 文件中追加一个定时任务，并将修改后的 conf 文件重新导入到 crontab 文件中，最后删除 conf 文件。
> 具体来说，命令分为三个部分：
1.  `crontab -l > conf`：将当前用户的 crontab 文件内容导出到 conf 文件。
2.  `echo "0 1 * * * /root/backupDockerDB.sh 3322" >> conf`：在 conf 文件中追加一个定时任务。
3.  `crontab conf`：将修改后的 conf 文件重新导入到 crontab 文件中，实现任务追加。最后使用 `rm -f conf` 命令删除 conf 文件。
