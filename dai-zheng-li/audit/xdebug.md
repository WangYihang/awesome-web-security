# xdebug



```text
sudo apt install php php-dev
sudo apt install php-xdebug
```

```text
sudo phpenmod xdebug
```

验证

```text
➜ php -m
[PHP Modules]
...
[Zend Modules]
Xdebug
Zend OPcache
```

修改 `php.ini`

```text
[XDebug]
xdebug.remote_enable = 1
xdebug.remote_autostart = 1
```

在 VSCode 中安装 PHP Debug 打开 Debug 窗口，创建 PHP 的 launch.json

```text
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "port": 9000
        },
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 9000
        }
    ]
}
```

修改配置

```text

```

参考文献 [https://xdebug.org/docs/remote](https://xdebug.org/docs/remote)

