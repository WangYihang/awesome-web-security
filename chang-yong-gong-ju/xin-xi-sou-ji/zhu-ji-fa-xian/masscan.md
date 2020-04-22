# masscan

This is an Internet-scale port scanner.**It can scan the entire Internet in under 6 minutes**, transmitting 10 million packets per second, from a single machine.

### 安装

```text
sudo apt install masscan
```

### 使用

```text
masscan 192.168.1.1 -p0-65535 --rate=10000
```

```text
masscan -p22,80,443,445,3306,1433,3389 192.168.1.1/24 --rate=10000
```

