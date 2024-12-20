# linux文件自动备份和保存

此方式为尝试自动保存mc服务器后台的数据，能够实现自动定期保存和定期删除多余的配置。除了mc服务器文件，其他类型都能按此方式进行定期备份。


首先手动测试一下备份指令能否正常执行：

创建文件夹：
``` bash
mkdir -p /home/danpe/mc/carpet_backup/auto_save/everyday/`date "+%Y-%m-%d"`
```
其中-p的意思是创建子文件夹路径。注意后面date格式中Y的大小写。
创建好后会自动生成一个随日期变化的文件夹，比如：/home/danpe/mc/carpet_backup/auto_save/2024-07-23/

然后使用tar指令生成压缩文件
``` bash
tar -zcvPf /home/danpe/mc/carpet_backup/auto_save/everyday/`date "+%Y-%m-%d"`/carpet_1.21.tar.gz /home/danpe/mc/carpet_1.21
```

一般来说，需要注意备份的文件内容是否都为用户的文件，而非root权限的文件，否则就会导致出错，导致部分文件无法备份。

在自己觉得合适的路径下，新建一个sh脚本文件：
``` bash
vim /home/danpe/mc/carpet_backup/everyday_backup.sh
```

填入以下内容：
``` bash
#!/bin/bash
source_folder=/home/danpe/mc/carpet_1.21
backup_folder=/home/danpe/mc/carpet_backup/auto_save/everyday/`date "+%Y-%m-%d"`
source_folder_name=`echo $source_folder |awk -F "/" '{print $3}'`.tar.gz
echo "source_folder：$source_folder"
echo "backup_folder: $backup_folder"
echo "source_folder_name: $source_folder_name"
# 新建立文件夹
mkdir -p /home/danpe/mc/carpet_backup/auto_save/everyday/`date "+%Y-%m-%d"`
# 压缩命令
tar -zcvPf $backup_folder/$source_folder_name  $source_folder
echo "$source_folder_name文件备份成功"
```

里面的路径可以根据自己的实际情况进行更换。

可以测试一下是否能正常运行：

``` bash
cd /home/danpe/mc/carpet_backup
chmod +x everyday_backup.sh
./everyday_backup.sh
```

编辑并添加到crond定时任务列表
``` bash
crontab -e
```

``` bash
20 3 * * * sh /home/danpe/mc/carpet_backup/everyday_backup.sh 2>&1 > /home/danpe/mc/carpet_backup/auto_save/everyday/log_$(date +\%Y-\%m-\%d)
```

然后重新启动crond即可：
``` bash
# CentOS等使用下面指令
/sbin/service crond restart
# Ubuntu/Debian等使用下面指令
/sbin/service cron restart
```

新建一个文件名为delete_everyday_backupfile.sh脚本，用以定时删除多余文件：
``` bash
#!/bin/bash
#待清除目录
dir=/home/danpe/mc/carpet_backup/auto_save/everyday/
#文件的过期周期
day_expireDay=10
#删除最终为day_expireDay前的备份文件与文件夹信息
find $dir -mtime +$day_expireDay | xargs rm -rf {}
echo "$dir下的$day_expireDay天前的文件清理成功"
```

然后添加到crond定时任务列表
``` bash
crontab -e
```
``` bash
03 4 * * * sh /home/danpe/mc/carpet_backup/delete_everyday_backupfile.sh 2>&1 > /home/danpe/mc/carpet_backup/auto_save/everyday/delete_log_$(date +\%Y-\%m-\%d)
```


