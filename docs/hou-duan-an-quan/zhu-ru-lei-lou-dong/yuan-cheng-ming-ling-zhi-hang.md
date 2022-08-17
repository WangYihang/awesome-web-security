# 远程命令执行

### 命令如何被执行？

命令组；管道；子命令（如 git --open-file-in-pager）；

Shell 的内置命令（[https://www.tldp.org/LDP/abs/html/internal.html](https://www.tldp.org/LDP/abs/html/internal.html)）

反引号

$\(\(\)\)

命令如何被注入？

判断是否可以注入

观察目标的被动响应（侧信道）

目标控制进行主动操作（发起请求）

### 场景分析

#### 有过滤

* 过滤空格
  * tab、${IFS}

#### 有回显

#### 无回显

* 有网络链接
  * **反弹 Shell**
  * 应用层协议（out of band）
    * HTTP 协议
      * curl
    * DNS 协议
      * dnslog
  * 网络层协议
    * ICMP 协议
* 无网络链接
  * 执行命令，将输出结果通过侧信道读出来
  * 侧信道
    * 时间信道
      * 将命令结果写文件，通过读取文件类似时间盲注入拿到命令执行结果（sleep命令、benchmark）
      * **二分查找**

辅助命令

* sed
* base64
* hex



