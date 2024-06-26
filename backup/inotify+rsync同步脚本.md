> rysnc是一个远程同步工具
> 
>  inotify是一种文件系统事件监控机制，包括添加、删除、移动、修改等各种事件
> 
>  **inotify+rsync** 可以实现监控某目录是否变动，进而增量备份同步

### Shell
<!--more-->
```shell
current_date=$(date +%Y%m%d_%H%M%S)
source_path=/tmp/src/
log_file=/var/log/rsync_client.log

#rsync
rsync_server=172.29.88.223
rsync_user=sean
rsync_pwd=/etc/rsync_client.pwd
rsync_module=module_test
INOTIFY_EXCLUDE='(.*/*\.log|.*/*\.swp)$|^/tmp/src/mail/(2014|20.*/.*che.*)'
RSYNC_EXCLUDE='/etc/rsyncd.d/rsync_exclude.lst'

#rsync client pwd check
if [ ! -e ${rsync_pwd} ];then
    echo -e "rsync client passwod file ${rsync_pwd} does not exist!"
    exit 0
fi

#inotify_function
inotify_fun(){
    /usr/bin/inotifywait -mrq --timefmt '%Y/%m/%d-%H:%M:%S' --format '%T %w %f' \
          --exclude ${INOTIFY_EXCLUDE}  -e modify,delete,create,move,attrib ${source_path} \
          | while read file
      do
          /usr/bin/rsync -auvrtzopgP --exclude-from=${RSYNC_EXCLUDE} --progress --bwlimit=200 --password-file=${rsync_pwd} ${source_path} ${rsync_user}@${rsync_server}::${rsync_module} 
      done
}

#inotify log
inotify_fun >> ${log_file} 2>&1 &
```
### 后台启动脚本即可

### 精简版
```
#!/bin/sh
/usr/local/bin/inotifywait -mrq -e modify,attrib,move,create,delete /test | while read file
do
    rsync -a --delete /test/ 192.168.1.20:/testbak/
    echo "$file在`date +'%F %T %A'`同步成功" >> /var/log/rsync.log
done
```