# HTTP 协议

### 简介

* 一种应用层协议
* 超文本传输协议
* 请求+响应
* 无状态（通过一些**其他特殊技巧**（Session）实现对状态的维护）
* 明文

### 格式

#### 请求

![](../.gitbook/assets/http-request-format.png)

![](../.gitbook/assets/http-request-example.png)

#### 响应

![](../.gitbook/assets/http-response-format.png)

![](../.gitbook/assets/http-response-example.png)

### 方法

* GET
* POST
* PUT
* DELETE
* HEAD
* OPTION

### 统一资源标识符（URI）

```text
URI = scheme:[//authority]path[?query][#fragment]
authority = [userinfo@]host[:port]
```

![](../.gitbook/assets/uri-dfa.png)

```text
http://admin:123456@www.example.com:8080/index.html?a=1&b=2#toc
```

### HTTP 协议版本

* HTTP/0.9 \(某些场景下可被用来绕过 WAF\)
* HTTP/1.0
* HTTP/1.1
* HTTP/2.0

### 常见请求头

* Host
* Cookie
* Referer
* User-Agent
* X-Forwarded-For

### HTTP 响应码

![](../.gitbook/assets/http-status-code.png)

### 常见响应头

* Set-Cookie
* Server

### 参考文献

* [RFC 2616 - Hypertext Transfer Protocol -- HTTP/1.1](https://datatracker.ietf.org/doc/rfc2616/)
* [https://www.freebuf.com/articles/web/93699.html](https://www.freebuf.com/articles/web/93699.html)



