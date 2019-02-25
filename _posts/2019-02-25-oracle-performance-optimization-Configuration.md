---
layout: post
#标题配置
title:  oracle性能优化的一些系统配置
#时间配置
date:   2019-02-25 20:01:00 +0800
#大类配置
categories: 日常笔记
#小类配置
tag: oracle
---

* content
{:toc}

修改进程数和连接数
---------------------
```sql
-- processes
alter system set processes=1000 scope=spfile;
-- sessions
alter system set sessions=1200 scope=spfile;
```

禁止sql tuning advisor
---------------------
```sql
begin
  dbms_auto_task_admin.disable
  (
    client_name => 'sql tuning advisor',
    operation   => null,
    window_name => null
  );
end;
/
```

创建好数据库后，将参数deferred_segment_creation改成FALSE
---------------------
```sql
alter system set deferred_segment_creation=FALSE scope=both;
```

关闭审计，同时删除已有的审计信息
---------------------
```sql
alter system set audit_trail=none scope=spfile;
truncate table aud$;
```

增加日志组文件，提高IO能力
---------------------
```sql
alter database add logfile group 4 ( '/home/oracle/oracle/oradata/ora11g/redo04_1.log') size 1024m;
alter database add logfile group 5 ( '/home/oracle/oracle/oradata/ora11g/redo05_1.log') size 1024m;
alter database add logfile group 6 ( '/home/oracle/oracle/oradata/ora11g/redo06_1.log') size 1024m;
alter database add logfile group 7 ( '/home/oracle/oracle/oradata/ora11g/redo07_1.log') size 1024m;
alter database add logfile group 8 ( '/home/oracle/oracle/oradata/ora11g/redo08_1.log') size 1024m;
alter database add logfile group 9 ( '/home/oracle/oracle/oradata/ora11g/redo09_1.log') size 1024m;
```