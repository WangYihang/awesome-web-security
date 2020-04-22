# Comment

考点：二次注入、源码泄漏、DS\_Store 解析、MySQL load\_file

### 信息搜集

发现 .git 目录 [http://192.168.174.131:8307/.git/config](http://192.168.174.131:8307/.git/config)

使用 GitHacker Dump 下源码

### 代码审计

在留言处存在二次注入

### 利用

1. 创建新帖

catagory= content=\*/\#

1. 在“详情”页面对该帖子进行留言（即触发二次注入） 内容为 \*/\#
2. 即可发现成功查出了 user\(\) 的结果
3. 尝试使用 load\_file 进行文件读取，读到 /etc/passwd

catalog=123',content=\(select\(load\_file\('/etc/passwd'\)\)\),/\*

1. 注意到 www 用户居然有家目录

![](2020-04-21-04-11-07.png)

1. 继续尝试读取该用户的 bash\_history
2. 看到有 DS\_Strore 文件，读取并进行解析
3. 发现 flag 文件
4. 读取 flag 文件

