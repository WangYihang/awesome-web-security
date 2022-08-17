# zmap

ZMap is capable scanning the entire public IPv4 address space in under 45 minutes.

### 使用

```text
sudo zmap -p 80 192.168.1.0/24 -i eth0
```

结果输出到 csv 文件

```text
-o results.csv
```

