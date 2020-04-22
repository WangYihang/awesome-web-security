# nmap

### nmap 是什么？

Nmap是一款开源免费的网络发现（Network Discovery）和安全审计（Security Auditing）工具。 软件名字Nmap是Network Mapper的简称。 Nmap最初是由Fyodor在1997年开始创建的。 随后在开源社区众多的志愿者参与下，该工具逐渐成为最为流行安全必备工具之一。

### 学习方法

查看文档 

查看 man 手册

### 基础概念

#### 扫描技术

* TCP 扫描
* SYN 扫描

#### 目标端口状态

* open（开放的）
* closed（关闭的）
* filtered（被过滤的）不确定开放还是关闭
* unfiltered （未被过滤的）
* openfiltered （开放或者被过滤的）
* closedfiltered （关闭或者未被过滤的\)

### 基础使用

默认扫描指定 IP

```text
nmap 192.168.1.1
```

探测目标操作系统版本

```text
nmap -O 192.168.1.1
```

扫描指定端口范围

```text
nmap -P 1-65535 192.168.1.1
```

扫描指定 IP 范围

```text
nmap -P 1-65535 192.168.1.1/24
```

使用 SYN 扫描

```text
nmap -sS -P 1-65535 192.168.1.1/24
```

### 高级使用

#### nmap script

对目标机器进行扫描,同时对smb的用户进行枚举

```text
nmap --script=smb-enum-users 192.168.1.1
```

对目标机器所开启的smb共享进行枚举

```text
nmap --script=smb-enum-shares 192.168.1.1
```

对目标机器的用户名和密码进行暴力猜测

```text
nmap --script=smb-brute 192.168.1.1
```

对目标机器测试心脏滴血漏洞

```text
nmap -sV --script=ssl-heartbleed 192.168.1.1
```

#### 快速批量扫描

```text
nmap -sS -Pn -n --open --min-hostgroup 4 --min-parallelism 1024 --host-timeout 30 -T4 -v -oG result.txt -iL ip.txt
```

```text
-Pn: Treat all hosts as online -- skip host discovery
-n/-R: Never do DNS resolution/Always resolve [default: sometimes]
--open: Only show open (or possibly open) ports
-T<0-5>: Set timing template (higher is faster)
--min-hostgroup/max-hostgroup <size>: Parallel host scan group sizes
--min-parallelism/max-parallelism <numprobes>: Probe parallelization
--host-timeout <time>: Give up on target after this long
-v: Increase verbosity level (use -vv or more for greater effect)
-d: Increase debugging level (use -dd or more for greater effect)
-oN/-oX/-oS/-oG <file>: Output scan in normal, XML, s|<rIpt kIddi3, and Grepable format, respectively, to the given filename.
-iL inputfilename (Input from list)
```

### 参考文献

* [https://www.jianshu.com/p/34bc564ca2ac](https://www.jianshu.com/p/34bc564ca2ac)
* `man nmap`

