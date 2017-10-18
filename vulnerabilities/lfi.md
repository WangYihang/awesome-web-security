# 文件包含漏洞

#### 1. 典型代码案例

```
<?php
    $file = $_GET['file'];
    include($file);
    // require($file);
    // include_once($file);
    // require_once($file);
?>
```

php 的文件包含针对于上述代码中的四个函数 :

> [http://php.net/manual/en/function.include.php](http://php.net/manual/en/function.include.php)
>
> [http://php.net/manual/en/function.require.php](http://php.net/manual/en/function.require.php)
>
> [http://php.net/manual/en/function.include-once.php](http://php.net/manual/en/function.include-once.php)
>
> [http://php.net/manual/en/function.require-once.php](http://php.net/manual/en/function.require-once.php)

文件包含函数不会检查被包含的文件是否是一个正常的 php 文件

只要包含了一个可以读的文件 , 那么它的内容就会被 php 的解释器执行

这也就是为什么图片木马可以执行的原因

#### 2. 文件包含与 phpinfo 结合导致 getshell

#### 3. 文件包含与文件上传结合导致 getshell

#### 4. 文件包含与 allow\_url\_include 结合导致 getshell

#### 5. 文件包含与日志文件结合导致 getshell

#### 6. 文件包含与 cgi 结合导致 getshell

#### 7. 文件包含与 segment fault 结合导致 getshell

#### 8. 文件包含与临时文件结合导致 getshell

#### 9. 文件包含导致敏感文件泄露

```
# locate 命令的数据库文件 , 保存了目标服务器的文件树
/var/lib/locatedb
```

#### 7. 总结

事实上可以看到在文件包含漏洞中 , 只要目标服务器上的某一个已知路径的文件内容可控 , 那么我们就可以利用文件包含功能去包含这个文件然后 getshell

#### 8. 参考文章

> [https://github.com/sektioneins/pcc/wiki/PHP-htaccess-injection-cheat-sheet\#example-1a-file-inclusion](https://github.com/sektioneins/pcc/wiki/PHP-htaccess-injection-cheat-sheet#example-1a-file-inclusion)
>
> https://github.com/bl4de/security\_whitepapers/blob/master/PHP\_LFI\_rfc1867\_temporary\_files.pdf
>
> https://github.com/bl4de/security\_whitepapers/blob/master/LFI\_testing\_techniques.pdf
>
> https://github.com/bl4de/security\_whitepapers/blob/master/LFI%20With%20PHPInfo%20Assistance.pdf
>
> https://github.com/bl4de/security\_whitepapers/blob/master/LFI-to-RCE.txt





