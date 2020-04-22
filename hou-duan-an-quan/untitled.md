# 文件包含漏洞

### 热身题

### 是什么？

程序结构化思想

### PHP 文件包含

PHP 特有的漏洞

* include
* include\_once
* require
* include\_once

include 和 require 语句是相同的，除了错误处理方面：

* require 会生成致命错误（E\_COMPILE\_ERROR）并停止脚本
* include 只生成警告（E\_WARNING），并且脚本会继续

如果被包含的文件内容中，存在 PHP OpenTag

* `<?php`
* `<?`
* `<?=`
* `<%`

  则 Tag 中包裹的内容将会被当做 PHP 代码**执行**

```php
<?php
include $_GET['type'].'_function'.php

/*
...
*/
?>
```

### 有什么危害？

* 任意文件读取
  * 如：包含 /etc/passwd、使用 PHP 伪协议读取源码

```text
?file=php://filter/read=convert.base64-encode/recource=index.php
```

* 远程代码执行！！！
  * 如：包含含有恶意代码的图片

PHP allow\_url\_include enable: 发送请求，并将结果包含（导致 SSRF） disable: 只能包含本地文件

### 有什么值得包含的文件？

一切用户可控的文件（包含（而不是读取）之后即可直接 getshell）

* 本地文件
  * 上传的图片、压缩包等
  * 上传一半的文件
  * Session
  * 日志
  * ...
* 远程文件
  * php://input
  * [http://vps/webshell.txt](http://vps/webshell.txt)

### 引入 PHP 语言特性（PHP 伪协议）

php://filter 元封装器，旨在当流打开的时候为应用提供对流进行过滤的功能 类似 Linux 的管道，可以多个配合使用 可用的过滤器有

* String Filters
  * string.rot13
  * string.toupper
  * string.tolower
  * string.strip\_tags（例题：by-pass-php-exit）
* Conversion Filters
  * convert.base64-encode
  * convert.base64-decode
  * convert.iconv.\*
* Compression Filters
  * zlib.deflate
  * zlib.inflate
  * bzip2.compress
  * bzip2.decompress
* Encryption Filters
  * mcrypt.\*
  * mdecrypt.\* 

php://input 只读流，可以让 PHP 脚本直接读取到 POST 的原始数据，而不是 $\_POST

phar:// PHP Archive 和压缩包类似，该 wrapper 可以读取 phar 文件中的数据

zip:// 该 wrapper 可以读取压缩包 zip://archive.zip\#dir/file.txt compress.zlib://file.gz compress.bzip2://file.bz2

### 例题

phar

### 参考文献

* [https://www.php.net/manual/en/filters.php](https://www.php.net/manual/en/filters.php)

