---
### 从账号
```
grant replication slave on *.* to slave@192.168.1.8 identified by '123456';
```
### my.cnf
<!--more-->
```
[mysqld]
port = 3306
datadir = /data
log_bin = /data/master-log-bin
log_bin_index = /data/master-log-bin.index
socket = /tmp/mysql.sock
expire_logs_days = 3
<!--more-->
open_files_limit = 10000
binlog_format =mixed 
# 很重要
server_id = 2
log_error = /data/log/master-error.log

lower_case_table_names=1
slave_type_conversions=ALL_NON_LOSSY
#从
slave-skip-errors =1756  
auto_increment_offset = 2
auto_increment_increment = 2
max_connections = 500
character-set-server = utf8mb4
wait_timeout = 120
#GTID配置
gtid_mode = on
#必须
enforce-gtid-consistency = true
binlog-do-db = shares3

log_slave_updates = on

slave-parallel-workers=0
master-info-repository = table
relay-log-info-repository = table

[mysql]
socket = /tmp/mysql.sock
```

*  数据冲突之列的复制错误，至于跳过事物Id本身，就不复杂了。

> (1)停止slave进程
> `mysql> STOP SLAVE;`
> 
> (2)设置事务号，事务号从Retrieved_Gtid_Set获取
> 在session里设置gtid_next，即跳过这个GTID
> 
> `mysql> SET GTID_NEXT= '6d257f5b-5e6b-11e8-b668-5254003de1b6:1'`
> 
> (3)设置空事物
> 
> `mysql> BEGIN; COMMIT;`
> 
> (4)恢复事物号
> 
> `mysql> SET SESSION GTID_NEXT = AUTOMATIC;`
> 
> (5)启动slave进程
> 
> `mysql> START SLAVE;`
> 
> 跳过一个事务之后，重启slave，恢复正常

* 对于master上的binlog被清理，slave上找不到对应的binlog，需要跳过主库上所有被清理的binlog

> 在主库执行 **show variables like '%gtid_purged%'**
> 
> 看主库清理的日志的范围，比如：6d257f5b-5e6b-11e8-b668-5254003de1b6:1-699578
> 
> 那么就要跳过主库上被清理的binlog的范围，需要设置从库上的gtid_purged的范围即可

```
> stop slave;
> reset master;
> set global gtid_purged='6d257f5b-5e6b-11e8-b668-5254003de1b6:1-699578';
> start slave;
```