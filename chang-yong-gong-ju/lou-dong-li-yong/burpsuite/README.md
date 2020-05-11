# BurpSuite

### 简介

Burp Suite 是用于攻击web 应用程序的集成平台。它包含了许多Burp工具，这些不同的burp工具通过协同工作，有效的分享信息，支持以某种工具中的信息为基础供另一种工具使用的方式发起攻击。这些工具设计了许多接口，以促进加快攻击应用程序的过程。所有的工具都共享一个能处理并显示HTTP 消息，持久性，认证，代理，日志，警报的一个强大的可扩展的框架。

### 配置

* Brup 默认监听 8080 端口（如果失败，检查是否被占用）
* 更换 Burp 端口
* 配置浏览器代理
* 添加 Burp 证书（HTTPs 网站）

### 功能

#### Intruder

可以暴力破解，如暴力破解管理员密码、验证码等

#### Repeater

重放 HTTP 流量包，对包进行细微的修改

#### Proxy

Burp 本身作为一个代理服务器，拦截客户端的所有请求，在拦截之后，用户可以对请求包进行：

* 修改
* 丢弃

等操作，也可以对响应包进行修改（需要特殊配置）。

#### Decoder

继承了 Base64、URL 等众多编解码器，并且可以配合串行使用。

* 类似 Unix 下的管道

#### Comparer

对比两个请求或者响应

### 插件

* [Copy As Python-Requests](https://github.com/portswigger/copy-as-python-requests)

### 参考文献

* [https://zhuanlan.zhihu.com/p/27545785](https://zhuanlan.zhihu.com/p/27545785)

